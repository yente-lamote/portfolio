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
        </p>
        <p>
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
    'Laravel', 'PHP', 'git', 'MySQL',
    'Deep learning', 'GraphQL', 'scss', 'Linux', 'PowerShell', 'HTML', 'Machine learning'
    ];
    const options = {
      // radius in px
      radius: window.innerWidth>950?window.innerWidth*0.17:window.innerWidth*0.3,

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
      transform: translateY(-49%);
      width: 100%;
      article{
        width: 38%;
        padding-top:2em;
        margin: auto auto auto 1rem;
        h1{
          font-size:4em;
        }
        p{
          margin-top:1rem;
          font-size:1.4em;
          color: $grey;
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
      aside{
        .tagcloud{
          right: 0% !important
        }
      }
    }
    color:white;
  }
  @media screen and (max-width: 1650px) {
        #about #about-container{
          article{
            width: 45%;
            h1{
              font-size:3em;
            }
            p{
              font-size: 1.3rem;
            }
          }
          aside{
            .tagcloud{
              right: 1% !important;
            }
          }
        }
        #face-wrapper{
            margin-right: 4em;
        }
    }

    @media screen and (max-width: 950px) {
      #about #about-container{
        padding: 2em 0;
        flex-direction: column-reverse;
        height: 80%;
        align-content: center;
        justify-content: center;
        article{
          width: 80%;
          height: 50%;
          margin: auto;
          margin-left: auto !important;
          margin-top:1.3em;
          padding-top: 0;
        }
        aside{
          height: 50%;
          .tagcloud{
            top:-9%;
            right: 0% !important;
            margin: auto !important;
          }
        }
      }
    }
  @media screen and (max-width: 500px) {
    #about{
      overflow: hidden;
      #about-container{
        padding: 2em 0;
        flex-direction: column-reverse;
        align-content: center;
        justify-content: center;
        height: auto;

        article{
          width: 72%;
            h1{
              font-size:1.9em;
            }
            p{
              font-size: 1rem;
            }
            #tiles-container{
              display: flex;
              .tile{
                padding:2rem 2rem 2rem 0;
                .tile-value{
                  display: block;
                  font-weight: 500;
                  font-size:2.1em;
                }
                .tile-subtitle{
                  font-size: 1rem;
                  font-weight: normal;
                }
              }
            }
        }
        aside{
          display: none;
        }
        
      }
    }
  }
</style>
