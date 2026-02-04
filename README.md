# Explyt Plugin Rules and Workflows

This repository contains rules and workflows for the Explyt plugin in IntelliJ IDEA.

## Overview

The Explyt plugin enhances IntelliJ IDEA with AI-powered development assistance. This repository provides:

- **Rules**: Configuration files that define how the Explyt plugin should behave in different scenarios
- **Workflows**: Predefined sequences of actions and templates for common development tasks

## Structure

- `rules/` - Contains rule definitions for the Explyt plugin
- `workflows/` - Contains workflow templates and configurations

## Usage

These rules and workflows are designed to be used with the Explyt plugin for IntelliJ IDEA. They help standardize development practices and automate common tasks through AI assistance.

## Getting Started

1. Install the Explyt plugin in IntelliJ IDEA
2. Go to ~/.explyt
3. Run 
```
git clone --filter=blob:none --no-checkout --depth 1 https://github.com/VaryaGet/explyt . && git sparse-checkout set rules workflows README.md && git checkout
```
4. Run to receive updates
```
git pull origin main --depth 1
```
5. Customize the configurations to match your team's development practices
