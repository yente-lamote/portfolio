<template>
  <section id="about">
    <div id="about-container">
      <article id="about-info">
        <h1>About Me</h1>
        <p>
          Hi, I'm Yente, a software developer based in Bruges. I'm 
          specialized in both back and font-end. I started programming 
          in 2016. Since then I have already gained some experience 
          from internships and school projects. The projects I enjoy
          working on are web applications and software with a lot 
          of functionality.
        </p><p>
          Besides software development I also have interests in 
          artificial intelligence and tech in general.
        </p>
        <div id="tiles-container">
          <div class="tile">
            <span class="tile-value">22</span>
            <span class="tile-subtitle">Years</span>
          </div>
          <div class="tile">
            <span class="tile-value"> 6</span>
            <span class="tile-subtitle">Years of experience</span>
          </div>
        </div>
        
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
    'MySQL', 'GraphQL', 'Git', 'Linux', 'PowerShell', 'HTML', 'scss'
    ];
    const options = {
      // radius in px
      radius: 300,

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
      display: flex;
      position: absolute;
      top:50%;
      transform: translateY(-50%);
      width: 100%;
      article{
        width: 38%;
        margin: auto auto auto 1rem;
        h1{
          font-size:4em;
        }
        p{
          margin-top:1rem;
          font-size:1.4em;
        }
        #tiles-container{
          display: flex;
          .tile{
            padding:2rem 2rem 2rem 0;
            .tile-value{
              display: block;
              font-weight: 500;
              font-size:3em;
            }
            .tile-subtitle{
              font-size: 1.2rem;
              font-weight: normal;
            }
          }
        }
        
        
      }
      .tagcloud{
        margin-left: auto;
        margin-right:4%;
      }
    }
    color:white;
  }
  @media screen and (max-width: 500px) {
    #about{
      overflow: hidden;
    }
  }
</style>
