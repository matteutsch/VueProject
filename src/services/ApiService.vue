<script lang="ts">
import { reactive } from "vue";
import type { User } from "../assets/User";

const data: any = reactive({ users: [] });

const baseurl = "https://reqres.in/api/users";

export const getAllUsers = async (): Promise<User[]> => {
  // Fetch data from page 1
  let respPage1 = await fetch(`${baseurl}?page=1`);
  let page1Data = await respPage1.json();
  data.users.push(...page1Data.data);

  // Fetch data from page 2
  let respPage2 = await fetch(`${baseurl}?page=2`);
  let page2Data = await respPage2.json();
  data.users.push(...page2Data.data);

  return data.users;
};

/* --------------------------------------------------------------- */

export const updateUser = async (userId: number, updatedUserData: User) => {
  let resp = await fetch(`${baseurl}/${userId}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(updatedUserData),
  });
  let updatedUser = await resp.json();
  return updatedUser;
};
/* --------------------------------------------------------------- */

export const createUser = async (newUserData: User) => {
  let resp = await fetch(baseurl, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(newUserData),
  });
  let newUser = await resp.json();
  return newUser;
};
/* --------------------------------------------------------------- */

export const deleteUser = async (userId: number) => {
  let resp = await fetch(`${baseurl}/${userId}`, {
    method: "DELETE",
  });
  return resp.ok;
};
</script>
