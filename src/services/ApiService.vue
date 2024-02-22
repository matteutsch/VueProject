<script lang="ts">
import { reactive } from "vue";

const data: any = reactive({ users: [] });

const baseurl = "https://reqres.in/api/users?page=";

export const getAllUsers = async () => {
  /* let resp = await fetch(url);
  data.users.data = await resp.json();
  return data.users.data; */

  // Fetch data from page 1
  let respPage1 = await fetch(`${baseurl}1`);
  let page1Data = await respPage1.json();
  data.users.push(...page1Data.data);

  // Fetch data from page 2
  let respPage2 = await fetch(`${baseurl}2`);
  let page2Data = await respPage2.json();
  data.users.push(...page2Data.data);

  return data.users;
};
</script>
