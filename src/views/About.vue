<template>
  <div class="about">
    <h1>About this project</h1>
    <p>
      SearchSurge makes it easy to tweak your search engine queries with
      operators like <code>site:stackoverflow.com</code>.
    </p>
    <p>
      Chaining many of these operators gives you search superpowers, but it's
      also a handful to type each time you want to allow or block many sites.
    </p>
    <p>
      With SearchSurge, you can manage your allowed and blocked sites with ease,
      switch between search modes and decide which search engine to use.
    </p>

    <h2>Where does my data go?</h2>
    <p>
      SearchSurge itself stores the sites you allow and block only to your web
      browsers local storage. No data is stored on any server. When you hit
      <i>Search</i> it takes the text you entered plus the urls you allowed or
      blocked, and opens a new tab to either Google or DuckDuckGo with the
      resulting search query.
    </p>

    <h2>Where can I learn more?</h2>
    <p>You can find the <a href="https://github.com/thutterer/searchsurge">source code</a> on GitHub.</p>
    <p>
      If you want to learn more about advanced search operators, checkout the
      <a href="https://youtube.com">video</a> that inspired this project.
    </p>
  </div>
</template>

<style scoped>
.about {
  color: #e8e8e8;
  padding: 0.5rem;
}

.about a {
  color: #63e2b7;
  text-decoration: none;
}
</style>
