<template>
  <div>
    <div class="blok-1 sitecontainer">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <h1 class="kurmetti">
              Дорогие гости!
            </h1>
            <h1 class="kurmetti_1">
              Приглашаем Вас <br>
              разделить с нами <br>
              праздник - <br>
              қыз ұзату <br>
              нашей дочери
            </h1>

            <h1 class="aida_title">
              Аиды
            </h1>
            <!--                      <h1 class="kurmetti_1 kurmetti_2">
                                    Тойына арналған <br>
                                    Дастарханымыздың қадірлі <br>
                                    Қонағы болуға шақырамыз!
                                  </h1>-->
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-12">
            <div class="abouttoi">
              <div class="toi1">
                Организаторы торжества
              </div>
              <div class="toi3">
                Малик и Ботагоз
              </div>
              <div class="toi4">
                2 августа 2025 года
              </div>
              <div class="toi4">
                17:00
              </div>
              <h1 class="toi1">
                Место проведения:
              </h1>
              <h1 class="toi3">
                город Хромтау<br>
                ресторан “GOLDEN PALACE”<br>
              </h1>
              <a target="_blank" href="https://2gis.kz/aktobe/geo/70000001082948707" class="twogis mt-3">Открыть на карте</a>
              <div style="    width: 100%;" />
              <div class="toi5">
                До начала торжества:
              </div>
              <div class="toi6">
                <div class="timer">
                  <div class="timer__items">
                    <div class="timer__item timer__days" data-title="дней" />
                    <div class="timer__item timer__hours" data-title="часов" />
                    <div class="timer__item timer__minutes" data-title="минут" />
                    <div class="timer__item timer__seconds" data-title="секунд" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="blok-1 sitecontainer">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <div class="prigtitle">
              Пожалуйста,<br>
              подтвердите свое присутствие:
            </div>
            <div id="form-1" class="container">
              <div class="row custom-center">
                <input type="hidden" name="shaqyruid" value="1787">
                <input type="hidden" name="konakid" value="0">

                <div class="radio-group">
                  <input
                      class="custom-radio"
                      type="radio"
                      value="Да, приду один (одна)"
                      id="contactChoice1"
                      name="zhauap"
                      v-model="selectedOption"
                  >
                  <label class="otvetyn" for="contactChoice1">Да, приду один (одна)</label>

                  <input
                      class="custom-radio"
                      type="radio"
                      value="Приду с супругой (-ом)"
                      id="contactChoice2"
                      name="zhauap"
                      v-model="selectedOption"
                  >
                  <label class="otvetyn" for="contactChoice2">Приду с супругой (-ом)</label>

                  <input
                      class="custom-radio"
                      type="radio"
                      value="К сожалению, не приду"
                      id="contactChoice3"
                      name="zhauap"
                      v-model="selectedOption"
                  >
                  <label class="otvetyn" for="contactChoice3">К сожалению, не приду</label>
                </div>
                <div class="col-12">
                  <input v-model="fio" class="inputname" type="text" name="name" placeholder="Ваше имя">
                  <button :disabled="isEmpty() || isSend" @click="sendShit" class="zayotrp">Отправить</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Toast from '@/components/Toast.vue';
import AudioPlayer from './AudioPlayer.vue';
import VerticalTimeline from './VerticalTimeline.vue';

export default {
  components: {
    Toast,
    AudioPlayer,
    VerticalTimeline
  },
  data() {
    return {
      selectedOption: "Да, приду один (одна)",
      fio: '',
      isSend: false,
    }
  },
  methods: {
    isEmpty() {
      if (!!this.fio === false) {
        return true
      } else {
        return false
      }
    },
    sendShit() {
      if (this.isSend) {
        return;
      }
      let variant = document.querySelector('input[name="zhauap"]:checked').value;
      let fio = this.fio
      let payload = "ФИО: " + fio + "\n" + "Выбрано: " + variant + "\n"
      this.sendMessage(payload)
    },
    sendMessage(payload) {
      const chatIds = ['379532768', '468944715'];
      const message = payload;
      const telegramBotToken = '7964082729:AAGsSmcgfLU8N0jDo1XJtzlSIGV8dradY7E';
      const url = `https://api.telegram.org/bot${telegramBotToken}/sendMessage`;


      chatIds.forEach(chatId => {
        axios.post(url, {
          chat_id: chatId,
          text: message,
        }).then(response => {
          //console.log('Message sent successfully:', response.data);
        })
            .catch(error => {
              //console.error('Error sending message:', error);
            });
      });
      // let  = document.querySelector('input[name="zhauap"]:checked').value;
      this.greet = ''
      this.fio = ''
      this.$bvToast.toast('Ақпарат той иелеріне жіберілді!', {
        title: 'Хабарлама!',
        noAutohide: true,
        appendToast: true,
        variant: 'success',
        solid: true,
      })
      this.isSend = true;
    },
    // },
  },
  mounted() {
    this.$nextTick(() => {
      // конечная дата
      //const deadline = new Date(2022, 11, 05, 18:00:00);
      const deadline = new Date(2025, 7, 2, 17, 0, 0);
      // new Date(yyyy, mm-1, dd, hh, mm, ss);
      // id таймера
      let timerId = null;

      // склонение числительных
      function declensionNum(num, words) {
        return words[(num % 100 > 4 && num % 100 < 20) ? 2 : [2, 0, 1, 1, 1, 2][(num % 10 < 5) ? num % 10 : 5]];
      }

      // вычисляем разницу дат и устанавливаем оставшееся времени в качестве содержимого элементов
      function countdownTimer() {
        const diff = deadline - new Date();
        if (diff <= 0) {
          clearInterval(timerId);
        }

        const days = diff > 0 ? Math.floor(diff / 1000 / 60 / 60 / 24) : 0;
        const hours = diff > 0 ? Math.floor(diff / 1000 / 60 / 60) % 24 : 0;
        const minutes = diff > 0 ? Math.floor(diff / 1000 / 60) % 60 : 0;
        const seconds = diff > 0 ? Math.floor(diff / 1000) % 60 : 0;

        const $days = document.querySelector('.timer__days');
        const $hours = document.querySelector('.timer__hours');
        const $minutes = document.querySelector('.timer__minutes');
        const $seconds = document.querySelector('.timer__seconds');
        if ($days && $hours && $minutes && $seconds) {
          $days.innerText = days < 10 ? '0' + days : days;
          $hours.innerText = hours < 10 ? '0' + hours : hours;
          $minutes.innerText = minutes < 10 ? '0' + minutes : minutes;
          $seconds.innerText = seconds < 10 ? '0' + seconds : seconds;
        }

        $days.dataset.title = declensionNum(days, ['дней', 'дней', 'дней']);
        $hours.dataset.title = declensionNum(hours, ['часов', 'часов', 'часов']);
        $minutes.dataset.title = declensionNum(minutes, ['минут', 'минут', 'минут']);
        $seconds.dataset.title = declensionNum(seconds, ['секунд', 'секунд', 'секунд']);
      }

      // вызываем функцию countdownTimer
      countdownTimer();

      const $days = document.querySelector('.timer__days');
      // const $dayscontent = document.querySelector('.dayscontent');
      // const $dayscontent2 = document.querySelector('.dayscontent2');
      // $dayscontent.textContent = $days.textContent;

      if (parseInt($days.textContent) > 100) {
        $days.textContent = '30';
      } else if (parseInt($days.textContent) > 70) {
        $days.textContent = '20';
      } else {
        $days.textContent = '10';
      }

      // $dayscontent2.textContent = $days.textContent;

      var discountprice = 18900 - 18900 * parseInt($days.textContent) / 100;
      discountprice = Math.round(discountprice / 10) * 10;
      discountprice = String(discountprice).replace(/(\d)(?=(\d{3})+([^\d]|$))/g, "$1 ");
      // $(".discountprice").text(discountprice);
      // const $dayscontent.dataset.title = $days.textContent;
      // вызываем функцию countdownTimer каждую секунду
      timerId = setInterval(countdownTimer, 1000);

      const button = document.querySelector('.zayotrp');

      button.addEventListener('click', function () {
        button.classList.add('clicked');
        button.disabled = true;

        // Simulating a delay before re-enabling the button
        setTimeout(function () {
          button.classList.remove('clicked');
          button.disabled = false;
        }, 500);
      });
    });
  }
}
</script>


<style type="text/css">

</style>
