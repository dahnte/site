<div class="container">
    <h1>web design</h1>
    <div class="item">
        <div>
            <img src="/ellen.png" alt="el lenador">
        </div>
        <div class="item-desc">
            <h1>El Leñador</h1>
            <p>Progressive web app, SEO optimization, automated backups with Updraft</p>
            <a href="https://www.ellenadornews.com" target="_blank" class="links">Website</a>
        </div>
    </div>
    <div class="item">
        <div>
            <img src="/nanasflan.png" alt="nanasflan">
        </div>
        <div class="item-desc">
            <h1>Nana's Flan</h1>
            <p>SvelteKit framework</p>
            <a href="https://nanasflan.github.io" target="_blank" class="links">Website</a>
            |
            <a href="https://github.com/nanasflan/nanasflan.github.io" class="links">Source code</a>
        </div>
    </div>
    <div class="item">
        <div>
            <img src="/dmsi.png" alt="DMSI">
        </div>
        <div class="item-desc">
            <h1>Diverse Male Scholar Initiative</h1>
            <p>UI layout</p>
            <a href="https://dmsi.humboldt.edu" target="_blank" class="links">Website</a>
        </div>
    </div>
    <h1 class="category">programming</h1>
    <div class="item">
        <div>
            <img src="/cproj.png" alt="README of c projects">
        </div>
        <div class="item-desc">
            <h1>Projects written in C</h1>
            <p>POSIX threads, ncurses library</p>
            <a href="https://github.com/dahnte/cs480" target="_blank" class="links">Source code</a>
        </div>
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: flex-start;
        width: 100%;
    }
    .item {
        display: flex;
        flex-direction: row;
        text-decoration: none;
        align-items: flex-start;
        color: var(--text-dark);
        padding: 0.5em;
        margin: 1em 0;
        border-radius: 0.5em;
        box-shadow: 0.3em 0.3em 0.8em var(--soft-shadow);
        width: 80%;
    }
    .item-desc {
        padding: 1em;
    }
    img {
        width: 280px;
        height: 280px;
        border-radius: 0.5em;
        border: none;
    }
    .links {
        text-decoration: none;
        font-size: 0.7em;
        color: var(--text-highlight-alt);
    }
    .links:hover {
        color:var(--text-highlight);
        transition: 0.6s;
    }
    .category {
        margin: 1.2em 0 0 0;
    }
    @media (max-width: 1024px) {
        img {
            width: 150px;
            height: 150px;
        }
        .container {
            justify-content: center;
            align-items: center;
        }
        .item {
            flex-direction: column;
            align-items: center;
        }
        * {
            font-size: 1em;
        }
    }
</style>