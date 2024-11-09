# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Yihan Liu

```
Please write your explanation here...

Step 1: 
    Event Sampling:
        Function used: simulate_event()
        Sample size: 1000
        Sampling frame: Population of 1000 individuals (where 200 at weddings, 800 at brunches)
        Distribution: Discrete uniform distribution
Step 2:
     Infection Sampling:
        Function used: np.random.choice()
        Sample size: 10% of population
        Sampling frame: 1000 individuals
        Distribution: Uniform random sample
Step 3: 
    Primary Contact Tracing:
        Function used: np.random.rand() < TRACE_SUCCESS
        Sample size: 20% of infected individuals
        Sampling frame: Infected individuals
        Distribution: Bernoulli distribution and p=0.2

Step 4:
     Secondary Contact Tracing:
        Function used: depend on the result in step 3
        Sample size: Infected individuals from events that more than two infections were traced.
        Sampling frame: Events with at least two traced infections

The blog explains that contact tracing disproportionately highlights large events, such as weddings, which are more likely to have multiple infections and traced contacts. The model in the code mirrors this bias by increasing the representation of larger gatherings in the traced data. As a result, smaller events, like brunches, are underrepresented despite similar infection rates, distorting the perceived sources of transmission and skewing the analysis of where infections primarily occur.

The shapes of the distributions are not similar. The blog graph displays a left-skewed distribution for the true proportion (blue) and a wider distribution for the observed proportion (red), indicating higher perceived infection rates in observed cases, while the given code produced a graph with a normal distribution. Additionally, the ranges on the x-axis are different, with the recreated graph showing a range up to around 0.35, and the original graph extending up to 1.0. This discrepancy may affect how closely the code replicates the visual effect intended in the original blog post.

The original plot displays a left-skewed distribution for the "Infections from Weddings" data, along with a broader, more dispersed distribution for the "Traced to Weddings" data. In comparison, the recreated graph (with a simulation size of 1000) presents both categories with roughly normal distributions. Additionally, in the recreated graph, the bars of the two distributions overlap considerably, whereas in the original graph, the bars are more clearly separated.

I will add np.random.seed. By introducing a seed, the random elements in the code, such as which individuals are infected or traced, will follow the same pattern each time the script is executed. This ensures that the results will be identical across multiple runs. 





```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
