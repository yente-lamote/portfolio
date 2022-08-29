<template>
  <section id="about">
    <div id="about-container">
      <article id="about-info">
        <h1>About</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum</p>
      </article>
      <aside>
        <span id="tagcloud"></span>
      </aside>
    </div>
  </section>
</template>
<script>
export default {
  mounted(){
    const container = '#tagcloud'
    const skills = [
    'JavaScript', 'Java', 'C#',
    'Python', 'ASP.NET', 'Vue.js', 'Node.js',
    'Laravel', 'PHP', 'Machine learning', 'Deep learning',
    'MySQL', 'GraphQL', 'Git', 'Linux', 'PowerShell'
    ];
    const options = {
      // radius in px
      radius: 200,

      // animation speed
      // slow, normal, fast
      maxSpeed: 'fast',
      initSpeed: 'fast',

      // 0 = top
      // 90 = left
      // 135 = right-bottom
      direction: 135,

      // interact with cursor move on mouse out
      keep: false
    };
    TagCloud(container, skills, options); 
  }
}
</script>
<style lang="scss">
  #about {
    #about-container{
      padding-top:15%;
      display: flex;
      article{
        position: absolute;
        top:50%;
        width: 40%;
        transform: translateY(-50%);
      }
      aside{
        position: absolute;
        top:50%;
        transform: translateY(-50%);
        right: 2%;
      }
      .tagcloud{
        margin-left: auto;
        margin-right:4%;
        margin-top:-8%;
      }
    }
    color:white;
  }
</style>
