<script>
    import { onMount } from "svelte";
    import RawCode from "./RawCode.svelte";
    import RawCode2 from "./RawCode2.svelte";
    import Card1 from "./Card1.svelte";
    import Card2 from "./Card2.svelte";
    import Card3 from "./Card3.svelte";
    import Card4 from "./Card4.svelte";
    import ReferencesCard from './ReferencesCard.svelte';
    import { writable } from "svelte/store";

    let currentSection = writable("Background"); // Reactive store
    const sections = ["Background", "Experiments", "Conclusion", "Contributions/Credits"];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        currentSection.set(entry.target.id); // Update reactively
                    }
                });
            },
            { threshold: 0.5 }
        );

        document.querySelectorAll("section").forEach((section) => {
            observer.observe(section);
        });
    });

    function scrollToSection(section) {
        
        document.getElementById(section).scrollIntoView({ behavior: "smooth" });
    }
</script>

<main>
    <nav>
        <ul>
            {#each sections as section}
                <li on:click={() => scrollToSection(section)} class="{$currentSection === section ? 'active' : ''}">
                    {section}
                </li>
            {/each}
        </ul>
    </nav>

    <section id="TODO" style="min-height: 10vh;">
        <div class="container">
            <h1 class="custom-title">Error Injection Robustness Classifier</h1>
        </div>
    </section>

    <section id="Background" style="min-height: 50vh;">
        <div class="container"><h1>Background</h1></div>
        <p>
            Pattern mining in this study is used to identify key structures within a dataset, 
            improving robustness measurement and error injection techniques. 
            The proposed method builds on previous work by learning dataset patterns efficiently and consistently across different datasets. 
            The process involves training a classifier, injecting errors into the data, applying robustness methods (favoring ZORRO over Meyer), 
            and evaluating robustness through numerical ratios and visualizations. 
            The heuristic pattern mining approach captures all possible predicates and inequalities, filtering out less relevant ones to refine error injection strategies. 
            This allows for a more effective robustness classifier that standardizes comparisons across datasets. 
            
        </p>
        <br>
        <h2>Method</h2>
        <RawCode  />

        <br>
        <h2>Heuristic Pattern Mining Influence Analysis</h2>
        <RawCode2  />
        
        
        
    <br>
    </section>
    <br>

    <section id="Experiments">
        <div class="container"><h1>Experiments</h1></div>

        <h2>Leave One Out</h2>

        
        <p>
            This following are the results of utilizing the leave one out method mentioned in section 2.1
to analyze the robustness ratios under given parameters for the below 2 datasets. Note per
section 2.3, robustness radius is declared for both datasets already with the MPG dataset
using a parameter of 2 and the insurance dataset using a parameter of 500. We’ll go into
further explanation behind the reasoning of setting these parameters at these key values in
the discussion section.
        </p>
        <Card1 />
    </section>


    
    <section id="Experiments">
        <h2>Heuristic Histogram</h2>

        
        <p>
            The following are the results of utilizing the discretization method mentioned in section 2.2
to analyze the robustness ratios under given parameters for the 2 datasets utilized in 3.1.1.

ZORRO is more consistent in maintaining a high robustness ratio across all conditions, 
while Meyer’s method shows greater variability, ranging from 100% to as low as 18.4%.
This suggests significant weaknesses in Meyer’s approach under certain conditions.
Based on the graph, ZORRO appears to be the more robust algorithm, consistently outperforming Meyer in robustness testing.
        </p>
        <Card2 />
    </section>

    
    <section id="Experiments">
         <h2>Pattern Mining</h2>

        
        <p>
            We utilized a pattern mining approach to identify all 
            possible patterns in a given dataset before filtering
            out the best patterns for error injection.
            ZORRO appears to be the more robust algorithm, consistently outperforming Meyer in robustness.
        </p>
        <Card3 />

    </section>

    <section id="Experiments">
         <h2>Normalization</h2>

        
        <p>
            We utilized normalization across methods and datasets to determine
            the most effective error injection for each dataset along with
            the comparison of robustness across datasets.
        </p>
        <Card4 />

    </section>

    <section id="Conclusion" style="min-height: 60vh;">
        <div class="container"><h1>Conclusion</h1></div>
        
        <p>
            We've showcased the usability of our model and how it can be used to gain
            an idea of the robustness of our chosen dataset compared to other sets.
            The next steps to further improve this work could 
            involve better scaling of robustness or exploring the
            specific numerical differences in robustness between sets.
        </p>
    </section>

    <section id="Contributions/Credits">
        <div class="container"><h1>Contributions/Credits</h1></div>
        
        <p>
            Joshua Huang led code optimization, setup, and test execution, assisted with report writing, and handled data gathering and cleaning.
            Marlon Garay contributed to code testing, report writing, and documentation, including the proposal, ethics, and schedule.
            Both collaborated on the website's design, visuals, and overall direction.

        </p>

        <br>

        <p>
        View the project on 
        <a href="https://github.com/rx-72/Dataset-Robustness-Classification-and-Error-Testing" 
           target="_blank" 
           rel="noopener noreferrer" 
           style="color: rgb(255, 225, 0); font-weight: bold;">
           GitHub
        </a>.
    </p>

    <ReferencesCard />
    </section>


</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap');
    
    :root {
        --color-bg: rgb(0, 0, 0);
        --color-text: rgb(255, 255, 255);
        --nav-bg: rgb(255, 225, 0);
        --nav-text: rgb(0, 0, 0);
        --nav-active: rgb(0, 0, 0);
    }

    :global(body) {
        background-color: var(--color-bg);
    }

    *,
    *::before,
    *::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    a {
    color: yellow;
    font-weight: bold;
    }

    body {
        background-color: var(--color-bg);
    }

    nav {
        background-color: var(--nav-bg);
        color: var(--nav-text);
        padding: 12px 24px;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        box-shadow: 0 25px 10px rgba(0, 0, 0, 0.75);
        z-index: 10;
        display: flex;
        justify-content: center;
    }

    nav ul {
        list-style: none;
        display: flex;
        gap: 20px;
    }

    nav li {
        font-family: 'Merriweather', serif;
        font-size: 22px;
        font-weight: 700;
        cursor: pointer;
        transition: color 0.3s ease, border 0.3s ease, background-color 0.3s ease;
    }

    nav li.active {
        color: var(--nav-active);
        border: 3px solid var(--nav-active);
        border-radius: 10px;
        background-color: rgb(255, 255, 255);
        padding: 3px 10px;
    }

    main {
        height: 100vh;
        padding: 80px 20px 20px;
        padding-top: 100px;
        font-family: 'Merriweather', serif;
        font-weight: 300;
        line-height: 1.5;
        font-size: 24px;
        color: var(--color-text);
        text-align: center;
    }

    section {
        padding: 20px 0; /* Ensures sections are large enough for the observer */
        min-height: 40vh; /* Adjust for better scrolling detection */
    }

    .custom-title {
        font-size: 50px;
        font-weight: bold;
        color: black;
        text-transform: uppercase;
        background: linear-gradient(to right, white, rgb(255, 255, 255));
        padding: 10px 20px;
        display: inline-block;
    }

    h1 {
        font-size: 40px;
        font-weight: 300;
        line-height: 1.2;
        margin-bottom: 20px;
        padding: 20px;
        background-color: var(--nav-bg); /* Background */
        color: var(--nav-text); /* Text color */
        display: inline-block; /* Ensures the background wraps the text */
        text-align: left; /* Aligns text inside */
        border-radius: 0; /* Keeps it squared */
        margin-left: 0; /* Ensures it aligns to the left */
    }

    h2 {
        font-size: 40px;
        font-weight: 300;
        line-height: 1.2;
        margin-bottom: 20px;
        text-align: left;
        padding-left: 20px;
    }

    /* If the parent is centering it, force left alignment */
    .container {
        text-align: left;
    }



    p {
        font-size: 20px;
        font-weight: 400;
        line-height: 1.6;
        text-align: left;
        padding-left: 20px;
    }
    
</style>
