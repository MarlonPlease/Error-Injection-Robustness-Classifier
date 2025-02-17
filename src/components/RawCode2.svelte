<script>
  let code = `

1. Each dataset feature has multiple possible patterns representing a sample size (e.g., temperature < 100°C covering 50% of the dataset).
2. We generate single-predicate patterns based on unique feature values in each column (e.g., for value "100" in a column, we create >, =, < conditions). This results in 3 * nk * k patterns, where nk is the number of unique values per column and k is the number of columns. We may bin values if uniqueness is too high.
3. We combine single-predicate patterns across different columns (e.g., temp > 100 with area < 50) but not within the same column. The max combination size is the number of columns, though we focus on 2-3 column combinations.
4. We filter pattern combinations using statistics like mean squared error, mean absolute error, or correlation to the target variable (y_train) to identify the most effective patterns.
5. The final set of patterns undergoes robustness testing with fixed parameters to simulate worst-case scenarios. Patterns with the lowest robustness ratio are selected as the most effective for representing the data and inducing label errors.

After identifying the top patterns for representation and error injection:

- We run ZORRO tests using the indexes these patterns capture for further analysis.
- We compare these results with prior methods, such as the naive approach and leave-one-out method from our previous paper.
- While pattern mining takes longer to determine the optimal indexes for maximum error, it proves to be a more effective approach—especially for datasets less sensitive to error injection.
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
