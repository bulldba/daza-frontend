<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <div class="row">
          <div class="col-sm-10">
            <h3>主题广场</h3>
          </div>
          <div class="col-sm-2 text-xs-right">
            <a class="btn btn-secondary btn-sm" v-link="{ name: 'topic_create' }">创建主题</a>
          </div>
        </div>
        <hr>
        <div class="row topic-list">
          <div class="col-md-4 col-sm-6" v-for="topic in topics">
            <div class="image">
              <img class="img-rounded" v-lazy="topic.image_url | thumbnail">
            </div>
            <div class="content">
              <a class="name" v-link="{ name: 'topic_detail', params: { id: topic.id } }">{{ topic.name }}</a>
              <small class="text-muted">{{ topic.subscriber_count }} 人订阅</small>
              <p class="description">{{ topic.description }}</p>
            </div>
            <hr>
          </div>
        </div>
        <!-- 分页导航 -->
        <vue-pagination :pagination="data.pagination" :callback="loadTopics"></vue-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import NProgress from 'nprogress';
import { auth } from '../../vuex/getters';
import { getTopicList } from '../../vuex/actions';
import VuePagination from '../_common/VuePagination';

export default {
  vuex: {
    getters: {
      auth,
      topics: state => state.topics.all,
    },
    actions: {
      getTopicList,
    },
  },
  data() {
    return {
      data: {
        pagination: {},
      },
    };
  },
  ready() {
    // 加载最新主题
    // NProgress.start();
    this.loadTopics(1);
  },
  route: {
    canReuse: false,
  },
  components: {
    VuePagination,
  },
  methods: {
    loadTopics(page) {
      NProgress.start();
      window.scrollTo(0, 0);
      // const query = {
      //   page,
      // };
      this.getTopicList(page).then(data => {
        this.data.pagination = data.pagination;
        NProgress.done();
      });
      // this.$route.router.go({ name: 'topic_list', query });
    },
  },
};
</script>

<style lang="scss" scoped>
.topic-list {
  list-style-type: none;
  padding: 0;
  div {
    .image {
      display: table-cell;
      vertical-align: top;
      img {
        width: 60px;
        height: 60px;
      }
    }
    .content {
      width: 10000px;
      display: table-cell;
      vertical-align: top;
      padding-left: 12px;
      .name {
        font-size: 14px;
        display: table-cell;
      }
      .description {
        font-size: 12px;
        color: #bbb;
        margin-bottom: 2px;
        height: 32px;
        line-height: 16px;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
    }
  }
}
</style>
