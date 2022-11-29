<script setup>
import { ref } from 'vue';
import dayjs from 'dayjs';

defineProps({
  data: Object,
});

const count = ref(0);
</script>

<template>
  <!-- {{ data }} -->
  <table
    style="
      position: relative;
      margin: auto;
      background-color: white;
      text-align: left;
      font-family: Roboto, Arial, sans-serif;
      box-shadow: 1px 3px 10px #b2b2b2;
    "
    width="400px"
  >
    <tbody>
      <tr>
        <td style="width: 60px; text-align: center; vertical-align: top">
          <div
            :style="`
              background-image: url(${data.logo});
              width: 40px;
              height: 40px;
              background-size: contain;
              background-repeat: no-repeat;
              background-position: center;
              margin: 5px 10px 0 10px;
              border-radius: 100%;
            `"
          ></div>
        </td>
        <td>
          <div style="display: block">
            <div
              style="
                margin-top: 5px;
                line-height: 20px;
                font-size: 14px;
                font-weight: bold;
                display: inline-block;
                letter-spacing: 0.25px;
              "
            >
              Existing Sender Name
            </div>
            <div
              style="
                float: right;
                font-size: 14px;
                margin: 5px 5px 0 5px;
                color: #5f6368;
                font-weight: bold;
              "
            >
              Expires&nbsp;
              <div style="color: #fa7b17; display: inline">tomorrow</div>
            </div>
          </div>
          <div
            id="subject-line"
            style="
              width: 324px;
              line-height: 20px;
              font-size: 14px;
              font-weight: bold;
              display: inline-block;
              white-space: nowrap;
              overflow: hidden;
              text-overflow: ellipsis;
            "
          >
            {{ data.subject }}
          </div>
          <div
            style="
              font-size: 14px;
              white-space: nowrap;
              max-width: 320px;
              display: flex;
              align-items: center;
              letter-spacing: 0.25px;
            "
          >
            <div
              style="
                background-color: #e6f4ea;
                padding: 2px 4px;
                color: #34a853;
                font-weight: 500;
                border-radius: 4px;
                display: inline-block;
                overflow: hidden;
                text-overflow: ellipsis;
                margin: 0 8px 0 0;
              "
            >
              {{ data.description }}
            </div>
            <div
              style="
                color: #5f6368;
                display: inline-block;
                font-weight: 500;
                margin: 0px 5px 0px 0px;
              "
            >
              Code
            </div>
            <div
              style="
                background-color: #f1f3f4;
                padding: 2px 4px;
                color: #3c4043;
                border-radius: 4px;
                font-weight: 500;
                display: inline-block;
                overflow: hidden;
                text-overflow: ellipsis;
              "
            >
              {{ data.discCode }}
            </div>
          </div>
          <div
            :style="`
              background-image: url(${data.image});
              width: 324px;
              height: 83px;
              background-size: cover;
              background-position: center;
              border-radius: 5px;
              margin: 6px 0px;
            `"
          ></div>
        </td>
      </tr>
      <tr>
        <td colspan="2"></td>
      </tr>
    </tbody>
  </table>
  <div
    style="
      margin-top: 10px;
      text-align: center;
      font-size: 10px;
      color: #9aa0a6;
    "
  >
    This is not a guarantee of how your email will be previewed.
  </div>
</template>

<style scoped></style>
