<template>
  <div id="footer">
      <div>
          <a href="https://hkplay.space">&copy; hkplace.space</a>
      </div>
      <div>May 2020</div>
  </div>
</template>

<script>
export default {
    name: 'Footer',
    components: {
    }
}
</script>

<style>
#footer {
    margin-top: 5rem;

    display: flex;
    flex-direction: row;
    align-items: center;

    color: var(--text-colour-dark);
}

#footer a, a:visited {
    text-decoration: none;
    color: var(--text-colour-dark);
}

#footer div:nth-child(1) {
    padding: 0.5rem;
}
</style>
