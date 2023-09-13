<div class="container">
    <div class="navbar">
        <nav>
            <a href="/site">Home</a>
            <a href="/blog">Blog</a>
        </nav>
    </div>

    <div class="content">
        <slot />
    </div>

</div>

<style>
    .container {
        display: flex;
        justify-content: center;
    }

    .navbar a {
        text-decoration: none;
        display: block;
        color: #000000;
    }

    .navbar a:hover {
        background-color: #e0e0e0;
    }
</style>