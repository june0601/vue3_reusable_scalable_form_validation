<template>
  <section class="signup-view">
    <form @submit.prevent novalidate class="ui form">
      <div class="ui stacked segment">
        <EmailField v-model="user.email" />
        <PasswordField v-model="user.password" />
        <button
          class="ui button red fluid"
          :disabled="isSignupButtonDisabled"
          @click="loginButtonPressed"
        >
          LOG IN
        </button>
      </div>
    </form>
  </section>
</template>

<script>
import { reactive } from "vue";
import EmailField from "@/components/EmailField";
import PasswordField from "@/components/PasswordField";

import useFormValidation from "@/modules/useFormValidation";
import useSubmitButtonState from "@/modules/useSubmitButtonState";

export default {
  components: {
    EmailField,
    PasswordField,
  },
  setup() {
    let user = reactive({
      email: "",
      password: "",
    });

    const { error } = useFormValidation();
    const { isSignupButtonDisabled } = useSubmitButtonState(user, error);

    const loginButtonPressed = () => {
      console.log(user);
    };

    return {
      user,
      isSignupButtonDisabled,
      loginButtonPressed,
    };
  },
};
</script>