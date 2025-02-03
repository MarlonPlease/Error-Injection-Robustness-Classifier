<script>
    import { onMount } from "svelte";
    import Card1 from "./Card1.svelte";
    import { writable } from "svelte/store";

    let currentSection = writable("Background"); // Reactive store
    const sections = ["Background", "Leave One Out"];

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

    <section id="Background" style="min-height: 60vh;">
        <h1>Background</h1>
        <p>
            This presentation focuses on exploring techniques and fill-in-word practices for ensuring data robustness.
        </p>
    </section>

    <section id="Leave One Out">
        <h1>Leave One Out</h1>
        <Card1 />
        <p>
            We discuss strategies for enhancing data quality and mitigating risks associated with unreliable datasets.
        </p>
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

    h1 {
        font-size: 40px;
        font-weight: 300;
        line-height: 1.2;
        margin-bottom: 20px;
        text-align: left;
        padding-left: 20px;
    }

    p {
        font-size: 20px;
        font-weight: 400;
        line-height: 1.6;
        text-align: left;
        padding-left: 20px;
    }
</style>
