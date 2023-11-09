<div class="container">
    <div class="navbar">
        <nav>
            <a href="/site">Home</a> <!-- when releasing for deployment change to "/site" -->
            <a href="/blog">Blog</a>
            <a href="/liero">Liero</a>
        </nav>
    </div>

    <div class="content">
        <slot />
    </div>
</div>

<footer>
    <p>Copyright © 2023 dahnte. <em>Is this necessary?</em></p>
</footer>

<style>
    .container {
        display: flex;
        justify-content: center;
        flex-direction: row;
    }

    .navbar {
        margin-right: 1em;
    }

    .navbar a {
        display: block;
        text-decoration: none;
        color: #000000;
        font-size: 1.5em;
        padding: 0.15em 0.15em 0.15em 0.8em;
        text-align: right;
    }

    .navbar a:hover {
        background-color: #e0e0e0;
        transition: background-color .3s;
    }

    .content {
        font-size: 1.4em;
    }

    footer {
        display: block;
        text-align: center;
    }
</style>