<template>
  <div class="home">
    <HelloWorld></HelloWorld>
    <ul>
				<li v-for="(item, i) in list" :key="i">
					<p v-html="item.question"></p>
          <form>
            <ul>
              <li v-for="(it, i) in item.incorrect_answers" :key="i">
                <label>
                  <input type="radio" > {{it}}
                </label>
              </li>
              <li>
                <label>
                  <input type="radio"> {{item.correct_answer}}
                </label>
              </li>
            </ul>
          </form>
          <p></p>
				</li>
			</ul>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'home',
  data() {
      return {
        info: null,
        list: null,
        option: null
      }
    },
  methods: {
		getUsers: function() {
			var vm = this;
			axios.get('https://opentdb.com/api.php?amount=10&category=21&difficulty=easy&type=multiple').then(function(response) {
        vm.list = response.data.results;
        console.log(vm.list)
			}, function(error) {
				console.log(error.statusText);
			});
		}
	},
	mounted: function() {
		this.getUsers();
	},
  components: {
    HelloWorld
  }
}
</script>
