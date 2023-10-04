<template>
  <section>
    <img id="logo" src="https://campaigns.cainandabelddb.com/img/logo.796b4e7a.svg" alt="cain&abelDDB logo">
    <div class="home">
      <div id="heading">
        <div id="title" ref="title">Banner1</div>

        <div id="description" ref="description">blah blah balh</div>
      </div>
      <div id="mediaHolder" ref="mediaHolder">
      </div>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src
import portfolio from '@/data/portfolioItems';

export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      mediaPlayer: null,
    };
  },
  methods: {
    checkAndSetMediaPlayer(item) {
      if (item.type === 'Banner') {
        this.mediaPlayer = document.createElement('iframe');
        this.mediaPlayer.setAttribute('src', item.source);
        this.mediaPlayer.setAttribute('height', item.height);
        this.mediaPlayer.setAttribute('width', item.width);
        this.mediaPlayer.setAttribute('frameBorder', 0);
        this.$refs.mediaHolder.appendChild(this.mediaPlayer);
      }
    },
    runPortfolio() {
      console.log(portfolio);
      // console.log(this.$refs.title.innerHTML);
      let counter = 0;
      this.$refs.title.innerHTML = portfolio[counter].name;
      this.$refs.description.innerHTML = portfolio[counter].description;
      this.checkAndSetMediaPlayer(portfolio[counter]);
      counter += 1;
      // set Initial value
      setInterval(() => {
        // tear down previous work
        this.mediaPlayer.remove();
        this.mediaPlayer = null;
        // Set title and description
        this.$refs.title.innerHTML = portfolio[counter].name;
        this.$refs.description.innerHTML = portfolio[counter].description;
        // actually mount the bloody work
        this.checkAndSetMediaPlayer(portfolio[counter]);

        // use counter to loop around array.
        counter += 1;
        if (counter > portfolio.length - 1) {
          counter = 0;
        }
      }, (portfolio[counter].time * 1000 + 2000));
    },
  },
  mounted() {
    this.runPortfolio();
  },
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  max-width: 1200px;
  /* align-items: center; */
  margin: 0 auto;
}

#logo {
  position: absolute;
  bottom: 1vh;
  right: 1vw;
  width: 100px;
  height: auto;
}

#heading {
  max-width: 1200px;
  text-align: left;
  display: flex;
  flex-direction: column;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

#title {
  font-size: 40px;
  line-height: 1.2;
  letter-spacing: 0.1em;
  font-weight: 600;
  margin-bottom: 1rem;
}

#description {
  font-size: 24px;
}

</style>
