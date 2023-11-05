<script setup>
//-4083601182
//
import {ref} from "vue";

const name = ref('');
const question = ref('');
const phone = ref('');
const email = ref('');
const success = ref(false);

async function onSubmit() {
  console.log(name.value,
      question.value,
      phone.value,
      email.value)
  const botToken = '6149915276:AAEZOWItpyTk77pHV97zGVB8BTRHel9RGrQ';
  const chatId = '-1002014961574';
  const text = 'Новое сообщение:%0A%0A' +
      `Вопрос: ${question.value}%0A` +
      `Имя: ${name.value}%0A` +
      `Телефон: ${phone.value}%0A` +
      `Эл. Почта: ${email.value}%0A `;

      await fetch(`https://api.telegram.org/bot${botToken}/sendMessage?chat_id=${chatId}&text=${text}`)
          .then((responce) => {
        if (responce.status === 200) {
          success.value = true;
        }
      })
          .catch((error)=>{
        success.value = false;
            console.log(error)
      })
  const massage = success.value ? 'Отправлено!' : 'Произошла ошибка, попробуйте позже!';
      alert(massage);
      name.value = '';
      question.value = '';
      phone.value = '';
      email.value = '';
}
</script>

<template>
  <section class="feedback">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-xl-6">
          <div class="feedback__text">
            <h2>Остались вопросы?</h2>
            <p>Свяжитесь с нами</p>
          </div>
        </div>
        <div class="col-lg-9 col-xl-6">
          <form class="form" method="post" @submit.prevent="onSubmit">
            <label class="mb-3">
                            <textarea
                                id="textarea"
                                placeholder="Введите ваш текст"
                                title="Введите ваш вопрос"
                                v-model="question"
                                required
                            >
                            </textarea>
            </label>
            <div class="form__group">
              <label>
                <input type="text"
                       placeholder="Ваше имя"
                       title="Введите ваше имя"
                       v-model="name"
                       required
                />

              </label>
              <label>
                <input type="tel"
                       placeholder="+7(___)___-____"
                       pattern="[0-9]{11}"
                       maxlength="11"
                       title="Номер телефона"
                       v-model="phone"
                       required
                />

              </label>
              <label>
                <input type="email" placeholder="Электронная почта"
                       title="Введите электронную почту"
                       v-model="email"
                       required
                />

              </label>
            </div>
            <button class="button-primary" type="submit">Отправить</button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>