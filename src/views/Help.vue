<template>
  <app-page back title="Помощь">
    <question-item
      v-for="q in questions"
      :key="q.title"
      :question="q"
    ></question-item>
  </app-page>
</template>

<script>
import AppPage from '../components/ui/AppPage'
import QuestionItem from '../components/question/QuestionItem'

export default {
  setup() {
    const questions = [
      {title: 'Что есть в данной системе', text: 'Тут есть просмотр заявок и их редактирование'},
      {title: 'Как работает авторизация', text:"Авторизация работает чере Firebase"}
    ]

    return {
      questions
    }
  },
  components: {AppPage, QuestionItem}
}
</script>
