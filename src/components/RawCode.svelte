<script>
  let code = `
We’ll use the following baseline for our classifier:
1. Train-test split the data that we want to gain a robustness measure on (80% train, 20% test).
2. Inject a specified percentage of targeted points in the y labels of the train data.
3. Utilize a chosen method (Meyer or ZORRO) to attempt to clean the error injection.
4. Evaluate robustness based on how well the cleaned train data performs on the test data.
5. Visualize findings using heat maps and line plots.

Tuning Parameters

- Uncertainty radius: The percentage of uncertainty injected into all targeted indices.
- Robustness radius: The range within which a perturbed point is still considered robust.
- Uncertainty Injection Percentage: The portion of the dataset affected by error injection.
  `;
</script>

<pre>{code}</pre>

<style>
  pre {
    background-color: rgba(255, 255, 255, 0);
    color: rgb(255, 255, 255);
    padding: 1rem;
    border-radius: 8px;
    overflow-x: auto;
    font-family: 'Merriweather', serif;
    
    
    white-space: pre-wrap;
    max-width: 1100px; /* Adjust width as needed */
    width: 100%;
    margin: 0 auto; /* Centers the block */

    font-size: 20px;
    font-weight: 400;
    line-height: 1.6;
    text-align: left;
    padding-left: 20px;
  }
</style>
