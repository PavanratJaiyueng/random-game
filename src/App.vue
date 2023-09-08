<script setup>
import { ref,} from 'vue'

const win_player1 = ref(0)
const draw_player1 = ref(0)
const loss_player1 = ref(0)

const win_player2 = ref(0)
const draw_player2 = ref(0)
const loss_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กระดาษ': 'แพ้',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'แพ้'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'เสมอ',
		'กรรไกร': 'แพ้',
    'ความรัก': 'แพ้'
	},
	'กรรไกร': {
		'ค้อน': 'แพ้',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'เสมอ',
    'ความรัก': 'แพ้'
	},
  'ความรัก': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'เสมอ'
	}

}



const player1 = ref('');
const player2 = ref('');
const result = ref('');

const img = {
  'ค้อน': 'https://scontent.fbkk29-1.fna.fbcdn.net/v/t1.15752-9/258389464_605857990861378_5054409703039041553_n.png?_nc_cat=100&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHckaaa3w1ZeSgKodehBSqsiQmwXKZXLaGJCbBcplctobunvjT7IGAbLml8JO_ZY89Y5BxwZ9ak_ECPezK1YeZ3&_nc_ohc=J4vSnCFi8lMAX9OvQDF&_nc_ht=scontent.fbkk29-1.fna&oh=03_AdReGOJnzZ3Hi32Kwjg43HuHdz-C9cpERhykTP-vxhbsmQ&oe=6521F0A1',
  'กระดาษ': 'https://scontent.fbkk29-7.fna.fbcdn.net/v/t1.15752-9/257931631_649927509338194_4873858528616916403_n.png?_nc_cat=108&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeFa3BjvZy9fa9q2GirDHwo2POAB90MlOTE84AH3QyU5MRiBMk1ZtgrxEjua2uSvCBgPhHO6kwRh6LUMoFvGnpr1&_nc_ohc=AvY_1KokLLEAX_dqba6&_nc_ht=scontent.fbkk29-7.fna&oh=03_AdQyvgyjJXhyZzqrfswqeW4Mt3nSBVeZdeXoGqvEYqnT_A&oe=652207FC',
  'กรรไกร': 'https://scontent.fbkk29-6.fna.fbcdn.net/v/t1.15752-9/257728672_918422625774466_8451502096658112685_n.png?_nc_cat=103&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeE0EkWenk571JTxgeEyJzAQnjxeTuBzSDSePF5O4HNINPlPGqhSV901Ejb5jeVy35UQdMN0IuUdZIEHICSY3ZsH&_nc_ohc=Kpq8rC9cJ-MAX_kqDJ0&_nc_ht=scontent.fbkk29-6.fna&oh=03_AdS8XsDLI1Lo_OzMonOLeQH865k6QjcdarsHwXGKt9exrg&oe=6521EE71',
  'ความรัก':'https://scontent.fbkk29-1.fna.fbcdn.net/v/t1.15752-9/373458397_6610892672357970_1029676300454193635_n.png?_nc_cat=100&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeGG_5NXSX930SWAXdoz1MpRX7qrEdzQ8d1fuqsR3NDx3QQ8JollVNaH5usKJXfVMcljYO8kTjRmDCQROOlWcCiD&_nc_ohc=feoVeTyEzeUAX81tWn7&_nc_oc=AQlrjS78u9K12TjuC_f2xi2rtwqVCPXNBdMaHW0dn3X503ExjjD_CU7Iwl5Vv4naEUk&_nc_ht=scontent.fbkk29-1.fna&oh=03_AdTJQchByoq6STYo7mIaoQkJ4ed16W1Sod0UdTZ4fJmtPQ&oe=6521F5F9'
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร','ความรัก'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1.value = getRandomChoice();
  player2.value = getRandomChoice();

  const out_result = control_game[player1.value][player2.value];

  if (out_result === 'ชนะ') {
    win_player1.value++;
    loss_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_player2.value++;
    loss_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_player1.value++;
    draw_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1.value = '';
  player2.value = '';
  result.value = '';
  win_player1.value = 0;
  draw_player1.value = 0;
  loss_player1.value = 0;
  win_player2.value = 0;
  draw_player2.value = 0;
  loss_player2.value = 0;
}

</script>

<template>

    <div class="box_title">
			<h1 class="text_title">เกมเป่ายิ๊งฉุบ</h1>
      </div>

      <div class="contrainer_game">
        <div class="box1" id="play1">
          <img v-if="player1" :src="img[player1]" alt="ผู้เล่นที่1 เลือก" class="img"/><br>
          ผู้เล่นที่1 ออก: {{ player1 }}
        </div>
        <div class="box2" id="play2">
          <img v-if="player2" :src="img[player2]" alt="ผู้เล่นที่2 เลือก" class="img" /><br>
          ผู้เล่นที่2 ออก : {{ player2 }}
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> เริ่มเกม </button>
    </div>

  <div class="contrainer_all_score"> 
    <div class="contrainer_score">
      <div class="box_score"> ผู้เล่นที่1 ชนะ <br> {{ win_player1 }}  </div>  
      <div class="box_score"> ผู้เล่นที่1 แพ้ <br> {{ loss_player1 }} </div>
      <div class="box_score"> เสมอ <br>{{ draw_player1 }} </div>
    </div>
    <div class="contrainer_score">
      <div class="box_score"> ผู้เล่นที่2 ชนะ <br> {{ win_player2 }}  </div>  
      <div class="box_score"> ผู้เล่นที่2 แพ้ <br> {{ loss_player2 }} </div>
      <div class="box_score"> เสมอ <br>{{ draw_player2 }} </div>
    </div>
  </div> 
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> เริ่มเกมใหม่ </button>
    </div>
   

</template>

<style>

@import url('https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@600&family=IBM+Plex+Sans+Thai:wght@400;600&family=Noto+Sans+Thai:wght@300&family=Taviraj:ital,wght@0,200;0,600;1,500&display=swap');



/*ALl body*/
:root {
  font-family: 'IBM Plex Sans Thai', sans-serif;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  background-image: linear-gradient( 95.2deg, rgba(173,252,234,1) 26.8%, rgba(192,229,246,1) 64% );

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  max-width: 1280px;
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}


/*background*/

.contrainer_game{
  display: grid;
  grid-template-columns: 1000fr 1000fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 20px;
  justify-content: space-between;
}

.img {
  width: 140px;
  height: 140px; 
}


.contrainer_score{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.contrainer_all_score{
  border:2px solid white;

  margin-left: 50px;
  margin-right: 50px;
}


.text_title{
  width: 500px;
  height: 70px;
  border-radius: 50px;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;  
  font-size: 32px;

}


.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-image: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  border-radius: 8px;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_new:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient(to right, #9796f0, #fbc7d4);


}


.buttom_start:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient(to right, #9796f0, #fbc7d4);
}


.buttom_start{
  padding: 20px;
  width: 9rem;
  height: 2.5rem;
  background-image: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.box_newgame,.start_buttom{
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
}

.img {
  width: 250px; /* Increase the width as needed */
  height: 250px; /* Increase the height as needed */
}

</style>