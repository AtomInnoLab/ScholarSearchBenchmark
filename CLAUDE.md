# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ScholarSearchBenchmark is a benchmark dataset for evaluating AI-driven academic paper validation, part of the [WisPaper](https://arxiv.org/abs/2512.06879) project by AtomInnoLab. Licensed under Apache-2.0.

## Dataset

The primary artifact is `wispaper_eval_100.json` — a 100-entry evaluation set spanning 10 academic domains (biology, chemistry, computer science, engineering, finance, math, medicine, neuroscience, physics, psychology).

Each entry contains:
- **paper_info**: metadata (title, authors, abstract, DOI, source URL, etc.)
- **criteria**: validation criteria the paper is judged against (described in natural language)
- **model_verification_results**: LLM-generated assessments with evidence and explanations
- **criteria_assessment**: human-annotated ground truth assessments
- **input**: the full prompt sent to the model for validation

Assessment values: `support`, `somewhat_support`, `reject`, `insufficient_information`.

Explanations are written in Chinese (中文). The benchmark tests whether models can correctly validate paper relevance against user-defined criteria.
