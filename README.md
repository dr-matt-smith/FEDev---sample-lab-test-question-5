[back to assessments](https://github.com/dr-matt-smith/FEDev---assessment-samples-and-walkthroughs?tab=readme-ov-file) <<<

[Question 1](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-1)
| [Question 2](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-2)
| [Question 3](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-3)
| [Question 4](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-4)
|
Question 5
| [Question 6](https://github.com/dr-matt-smith/FEDev---sample-lab-test-question-6)


# FEDEv - SAMPLE lab test question 5

The "brief" for the test is a PDF file in directory "brief"

NOTE:
**no use of AI is permitted in the lab test**

There are videos for each of the 6 questions:


The files in this repo are the solution I created to this sample test
- you may use any editor available on the university PCs
  - I used Celbridge, which you may install on the lab PCs if you wish

## Question 5 - video

- question 5
  - https://go.screenpal.com/watch/cOehrrnZFrc
  - 2mins 50secs


## Question 5 - create JSON file `/src/lib/data/foods.json`

First let's create the JSON data file

`/src/lib/data/foods.json`

```json
[
    {   "name": "lemon juice",
        "ph": 2
    },
    {   "name": "lettuce",
        "ph": 7
    },
    {   "name": "apples",
        "ph": 4
    }
]
```

Note, there is no semi-=colon `;` after the final close square-bracket `]` (this is a common error when copy-pasting JSON from a variable assignment into its own data file...)

## Question 5 - remove hard-coded variable and read in JSON file in Svelte script

We can now update our Svelte script (`/routes/food/+page.svelte`) to read the JSON data from the file into variable `foods`:

NOTE
- a common convention is to use plural nouns for arrays (e.g. `foods`), and singular nouns for the current item. when looking (e.g. `food`)

```html
<script>
    import { isNeutral } from '$lib/util/useful_functions.js';
    import foods from '$lib/data/foods.json';
</script>
```

That's it!

Since the variable name is the same, our look code doesn't need any refactoring.

`/routes/food/+page.svelte`

```html
<script>
  import { isNeutral } from '$lib/util/useful_functions.js';
  import foods from '$lib/data/foods.json';
</script>

<table>
  <tbody>

  {#each foods as food}
  <tr>
    <td>{food.name}</td>
    <td>{food.ph}</td>
    <td>
      {#if isNeutral(food.ph)}
      Neutral
      {:else}
      Acidic or alkaline
      {/if}
    </td>
  </tr>
  {/each}

  </tbody>
</table>

<style>
  table, td, tr  {
    border: 1px solid black;
  }

  td {
    padding: 1rem;
    width: 12rem;
    text-align: center;
  }
</style>
```