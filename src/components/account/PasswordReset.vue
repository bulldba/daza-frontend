<template>
  <div class="container">
    <div class="row">
      <div class="col-md-4 col-sm-3"></div>
      <div class="col-md-4 col-sm-6">
        <h3 class="text-xs-center">重置密码</h3>
        <validator name="validation">
          <form novalidate @submit.prevent="submit()">
            <div class="form-group">
              <label>我们将发送一封密码重置邮件到你的邮箱<br>点击按钮即可重置密码</label>
              <input class="form-control" type="email" name="email" placeholder="请输入邮箱" v-validate:email="rules.email">
            </div>
            <div class="form-group">
              <button type="submit" class="btn btn-primary btn-block" :disabled="!$validation.valid">发送验证邮件</button>
            </div>
          </form>
        </validator>
      </div>
      <div class="col-md-4 col-sm-3"></div>
    </div>
  </div>
</template>

<script>
import toastr from 'toastr';
import { auth } from '../../vuex/getters';
// import {  } from '../../vuex/actions';

export default {
  vuex: {
    getters: {
      auth,
    },
    actions: {
    },
  },
  data() {
    return {
      rules: {
        email: { required: true, email: true },
      },
      params: {
        email: '',
      },
    };
  },
  ready() {
  },
  methods: {
    submit() {
      toastr.warning('开发中，敬请期待！');
    },
  },
};
</script>

<style scoped>
</style>
