<!--
 * @Description: 
 * @Author: 曹俊
 * @Date: 2022-12-12 18:00:18
 * @LastEditors: 曹俊
 * @LastEditTime: 2022-12-15 18:09:01
-->

<template>
  <div class="container">
    <input id="document" type="file" />
    <div class="row">
      <div class="span8">
        <div id="output" class="well"></div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import mammoth from "mammoth";
import { onMounted } from "vue";
// import Demo from "./api/bug.js";
// const data = Demo();
// console.log(data, "data");
const main = () => {
  let doc = document.getElementById("document") as any;
  doc.addEventListener("change", handleFileSelect, false);
  doc.addEventListener("change", () => {
    const containerDiv = document.querySelector("div.container") as any;
    containerDiv.style.display = "none";
  });

  function handleFileSelect(event: any) {
    readFileInputEventAsArrayBuffer(event, function (arrayBuffer: any) {
      mammoth.convertToHtml({ arrayBuffer: arrayBuffer }).then(displayResult).done();
    });
  }

  function displayResult(result: any) {
    // 获取id为output的表格元素
    const outputElement = document.getElementById("output") as any;
    outputElement.innerHTML = result.value;
    const tableElement = outputElement.querySelector("table");
    const tbodyElement = tableElement.querySelector("tbody");
    console.log(tbodyElement, "tbodyElement");
    // 获取表格中的每一行
    const rows = tbodyElement.getElementsByTagName("tr");

    // 定义一个数组，用来保存表格中的内容
    const tableData = [];

    for (let i = 0; i < rows.length; i++) {
      // 获取每一行的所有单元格
      const cells = rows[i].getElementsByTagName("td");

      // 定义一个数组，用来保存每一行的内容
      const rowData = [];

      for (let j = 0; j < cells.length; j++) {
        // 获取单元格中的内容
        const cellContent = cells[j].innerHTML;

        // 将单元格中的内容添加到行数组中
        rowData.push(cellContent);
      }

      // 将行数组添加到总数组中
      tableData.push(rowData);
    }

    // 输出表格中的内容
    console.log(tableData);

    var messageHtml = result.messages
      .map(function (message: any) {
        return (
          '<li class="' + message.type + '">' + escapeHtml(message.message) + "</li>"
        );
      })
      .join("");
    let messages = document.getElementById("messages") as any;
    messages.innerHTML = "<ul>" + messageHtml + "</ul>";
    return tableData;
  }

  function readFileInputEventAsArrayBuffer(event: any, callback: any) {
    var file = event.target.files[0];

    var reader = new FileReader();

    reader.onload = function (loadEvent: any) {
      var arrayBuffer = loadEvent.target.result;
      callback(arrayBuffer);
    };

    reader.readAsArrayBuffer(file);
  }

  function escapeHtml(value: any) {
    return value
      .replace(/&/g, "&amp;")
      .replace(/"/g, "&quot;")
      .replace(/</g, "&lt;")
      .replace(/>/g, "&gt;");
  }
};
// main();
</script>

<style scoped></style>
