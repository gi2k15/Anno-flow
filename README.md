# Anno Flow Calculator

A small Vue 3 app that helps optimize production chains for **Anno** series.

You provide each industry/building and its production time (in seconds), and the app calculates the minimal building ratio needed to keep the chain balanced.

## What the project does

- Lets you add and remove buildings in a production chain
- Accepts predefined times (`30`, `60`, `90`, `120`) or a custom value
- Calculates an optimized flow ratio from all valid times
- Shows the exact number of required buildings for each step
- Supports reset to quickly start a new chain

## How calculation works

The app converts all valid production times to numbers and computes the **greatest common divisor (GCD)** across them.

For each building:

`required buildings = building time / GCD(all times)`

This produces the smallest whole-number ratio for the entire chain.

## Tech stack

- Vue 3 (Composition API + `<script setup>`)
- Vite
- pnpm

## Getting started

### Requirements

- Node.js `^20.19.0` or `>=22.12.0`
- pnpm

### Install dependencies

```sh
pnpm install
```

### Run in development mode

```sh
pnpm dev
```

### Build for production

```sh
pnpm build
```

### Preview production build

```sh
pnpm preview
```
