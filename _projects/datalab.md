---
title: "Fully locally hosted LLM tool for data analytics"
date: "2026-01-15"
category:
  - Software
  - Business & Analytics
description: "A LLM powered tool that lets users explore tabular data through a chat interface which is locally hosted and reproducable"
image: "/assets/images/datalab/datalab.png"
link: ""
---

Data science is one of those fields that feels like it should be more accessible than it is. The tools are mature, the techniques are well documented, and the potential value for data-heavy domains like medicine, education, public health, and business seems enormous. But in practice, a lot of the people who would benefit most from it don't have the technical background to use it. A nurse tracking patient outcomes, a school administrator trying to understand attendance patterns, a small business owner with years of transaction history sitting in spreadsheets: they all have data that could probably inform their decisions better, but getting from a CSV to an actual insight still requires knowing Python, SQL, or at minimum a specialized tool that fits their exact use case.

When I took ACMS 40876, Data Science in Practice: Tools and Applications, the final project was open-ended enough that I could try building something around this idea. I worked on it solo, which meant the scope had to be realistic, but it gave me room to actually think through the design rather than just shipping features.

## The Core Idea

The first instinct with something like this is usually to build a GUI with drag-and-drop charts and point-and-click filters. I considered it, but those tools tend to hit a ceiling fast. The moment a user wants something the interface didn't anticipate, they're stuck, and you end up building something that's easy for the simple cases and useless for anything more nuanced.

What seemed more promising was the fact that language models are pretty good at writing Python, especially for data science tasks. So instead of building a fixed interface on top of analysis tools, I tried letting the AI write the code and handing it directly to the user. The idea was that they'd get the expressive power of something like pandas and matplotlib without needing to know how to use either.

That's roughly how DataLab works. You load your data, describe what you want, and the AI writes the Python to do it. You can look over the code, change anything that seems off, and run it. The output appears inline. It's not a perfect solution, but as a first pass at the idea it seemed worth trying.

![DataLab chat interface](/assets/images/datalab/datalab.png)

## Why Keep It Local

One thing I kept coming back to was that the domains where this tool could be most useful are also the ones where sending data to a remote server is the hardest sell. Healthcare has compliance requirements. Schools have privacy obligations around student records. A lot of organizations are just cautious about business data leaving their machines at all.

Running everything locally sidesteps that problem. The data never leaves the machine. DataLab also supports fully offline models through Ollama, so in theory it could work in environments with no internet connection at all. Whether that's actually how people would use it is a different question, but it felt like the right default to build toward.

## Some of the Design Choices

A few decisions shaped how the project came together.

**Code instead of tools or direct answers.** My first instinct was to give the AI a set of predefined tools it could call, something closer to an MCP-style setup where it would invoke specific functions for loading data, running aggregations, generating charts, and so on. The problem was that smaller models that can actually run locally struggled with tool use. They'd call the wrong tool, pass malformed arguments, or just not recover well when something failed. And since the whole point was to support offline, locally hosted models, I couldn't just lean on a more capable API model to paper over those issues.

I briefly considered looping the model back in to fix its own mistakes automatically, but the tool-based approach had another problem: it was too opinionated. Every analysis task is slightly different, and trying to cover enough cases with a fixed set of tools would have meant either a bloated tool API or a tool that only handled the easy scenarios well.

What ended up working was just asking the model to write Python directly. Smaller models are noticeably better at code generation than at structured tool use, probably because they've seen so much more of it in training. The AI could express basically any analysis as a few lines of pandas or matplotlib, without needing to fit it into a predefined interface. From there, the engineering problem became about the infrastructure around the code: making sure the model had enough context about the dataset to write accurate code, keeping it aware of what variables were already in scope, and giving users a way to extend the environment with additional libraries or custom functions for more specialized workloads.

**A notebook-style format.** The interface ended up close to how Jupyter works, which wasn't entirely planned but made sense. The full session including all generated and edited code gets saved as a JSON file and reloads automatically. You can re-run from the top and get the same result, which is a useful property for anything that needs to be reproducible.

**Syncing the AI's context after each run.** A problem I ran into early was the model writing code that referenced variables that no longer existed, or missing columns that had been added. The fix was syncing the kernel namespace back to the backend after every execution, so the AI's view of the data stays current. It's a small thing but it made the tool a lot less frustrating to use.

**Tiered profiling for wide datasets.** Injecting the full column profile into every prompt works fine for narrow datasets but starts to break down with 60 or more columns. I ended up with a tiered strategy: full profile with sample values under 30 columns, no sample values from 30 to 59, and type-grouped summaries at 60 and above. It's not elegant but it kept the prompts from getting unwieldy.

---

## Under the Hood

DataLab connects a React frontend to a FastAPI backend managing two components: an LLM router and a persistent Jupyter kernel. The AI writes code against the standard Python data science stack:

| Library | Role |
|---|---|
| pandas | Data loading, filtering, groupby, joins, null handling |
| numpy | Array math, IQR and Z-score outlier bounds |
| matplotlib / seaborn | Distribution plots, heatmaps, scatter and bar charts |
| scipy | Hypothesis tests, correlation coefficients |
| scikit-learn | Train/test splitting, model fitting, evaluation metrics |
| DuckDB | SQL queries directly against in-process DataFrames |

There's also a Functions tab where users can write custom Python helpers stored as plain `.py` files. The AI reads each function's docstring and calls it when relevant, which could be useful for domain-specific workflows, though I didn't get to test that much in practice.

## What It Can Do

- Load CSV, Excel, or JSON with automatic profiling on drop
- Identify missing values, detect outliers via IQR and Z-score, fill nulls, remove duplicates
- Generate summary statistics, distribution analyses, and correlation matrices
- Render heatmaps, histograms, and grouped bar charts inline
- Fit and evaluate machine learning models via scikit-learn

| ![DataLab analysis output](/assets/images/datalab/datalab_output.png) | ![DataLab chart example](/assets/images/datalab/datalab_plot.png) |

## Limitations and What Could Come Next

The reliability issues are real. Smaller local models sometimes produce code that looks correct but has logic errors, especially on wider datasets where the model only has a partial view of what it's working with. The tool also assumes users can tell when generated code is wrong, which isn't always a safe assumption.

There's a lot that would make it more useful: multi-table support, the ability to export notebooks as PDF or HTML, better handling of large files. The more important thing, though, would be actually testing it with non-technical users in a real context to see where it breaks down. The class project format didn't leave much room for that, so a lot of what I think about how well it works is still somewhat speculative.
