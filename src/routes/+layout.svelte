<div class="grid">
    <div>
        <nav>
            <a href="/showcase">showcase</a>
        </nav>
    </div>

    <div class="content">
        <slot />
    </div>
</div>


<style>
    .grid {
        display: grid;
        grid-template-columns: 20vw 80vw;
        font-size: 1.5em;
        color: var(--text-dark);
    }
    nav {
        display: flex;
        flex-direction: column;
        text-align: right;
        margin: 1em;
    }
    nav a {
        text-decoration: none;
        color: var(--text-dark);
    }
    nav a:hover {
        color: var(--text-highlight);
        transition: 0.6s;
    }
    .content {
        margin: 1em;
    }
    @media (max-width: 1024px) {
        .grid {
            grid-template-columns: auto;
        }
        nav {
            text-align: center;
        }
    }
</style>