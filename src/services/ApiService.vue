<script lang="ts">
import { reactive } from "vue";

const data: any = reactive({ users: [] });
const url = "https://reqres.in/api/users?page=1";

export const getAllUsers = async () => {
  let resp = await fetch(url);
  data.users.data = await resp.json();
  return data.users.data;
};
</script>
