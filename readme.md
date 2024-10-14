## Retro Forum

## live link:[ https://hasanali44.github.io/forum-retro/]

```
const allPost = async () => {
  const res = await fetch(
    `https://openapi.programming-hero.com/api/retro-forum/posts`
  );
  const data = await res.json();
  displayShow(data.posts);
};

const displayShow = (posts) => {
  const allPost = document.getElementById("all-post");
  allPost.textContent = "";
  posts.forEach((post) => {
    // console.log(post);
    const card = document.createElement("div");
    card.classList =
      "bg-[#797DFC1A] w-[772px] h-[270px] rounded-2xl py-10 px-10 mb-10";
    card.innerHTML = `
    <div
            class=""
          >
            <div class="flex w-full">
            <div class="relative">
            ${
              post?.isActive
                ? ` <div class="bg-green-700 w-3 h-3 rounded-full absolute -top-1 -right-2 border-2 border-white "></div>`
                : `<div class="bg-red-700 w-3 h-3 rounded-full absolute -top-1 -right-2 border-2 border-white "></div>`
            }
              <img class="w-16 h-14 rounded-sm" src="${post.image}" alt="" />
              </div>
              <div class="pl-6 w-full">
                <p  class="text-sm">
                  <span class="font-bold pr-2"># ${post.category}</span> ${
      post.author.name
    }
                </p>
                <h3 class="text-xl font-bold py-3">
                  ${post.title}
                </h3>
                <p>
                  ${post.description}
                </p>
                <div class="border border-dashed border-black/20 mt-10"></div>
                <div class="mt-5 flex justify-between ">
                <div>
                  <span>
                    <i class="fa-regular fa-message mr-2"></i>
                   ${post.comment_count}
                  </span>
                  <span class="ml-5">
                    <i class="fa-regular fa-eye mr-2"></i>
                    ${post.view_count}
                  </span>
                  <span class="ml-5">
                    <i class="fa-regular fa-clock mr-2"></i>
                   ${post.posted_time} min
                  </span>
                  </div>
                  <div>
                  <button onclick="handleRead(${post.id})" >
                  <i class="fa-regular fa-envelope-open bg-green-700 text-white p-2 rounded-full"></i>
                  </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
    `;
    allPost.appendChild(card);
  });
};
// count
let count = 1;
const handleRead = async (id) => {
  const res = await fetch(
    `https://openapi.programming-hero.com/api/retro-forum/posts?id=${id}`
  );
  const data = await res.json();
  const allPost = data.posts;
  const post = allPost.find((post) => post.id == id);
  console.log(post);
  const markRead = document.getElementById("mark-read");
  const card2 = document.createElement("div");
  card2.classList =
    "flex justify-between bg-white mt-5 mb-5  py-3 px-3 rounded-xl";
  card2.innerHTML = `

              <p>
                ${post.title}
              </p>
              <div class="">
                <span>
                  <i class="fa-regular fa-eye mr-2 pt-1"></i>
                  ${post.view_count}
                </span>
              </div>

  `;
  markRead.appendChild(card2);
  const countText = document.getElementById("count");
  countText.innerText = count++;
};
allPost();

// latest post
const blogCard = async () => {
  const res = await fetch(
    `https://openapi.programming-hero.com/api/retro-forum/latest-posts`
  );
  const data = await res.json();
  displayBlogShow(data);
};

const displayBlogShow = (blogs) => {
  // console.log(blogs);
  const latestPosts = document.getElementById("blog-card");
  blogs.forEach((blog) => {
    const blogCard = document.createElement("div");
    blogCard.classList = "border px-8 py-8 rounded-xl";
    blogCard.innerHTML = `
  <div  class="">
          <img class="w-[326px] h-[190px] rounded-xl" src="${
            blog.cover_image
          }" alt="" />
          <div class="pt-3">
            <p>${
              blog.author.posted_date
                ? blog.author.posted_date
                : "No publish date"
            }</p>
            <h4 class="font-bold text-xl py-2">
             ${blog.title}
            </h4>
            <p>
             ${blog.description}
            </p>
            <div class="pt-6 flex">
              <img class="w-11 h-11 rounded-full" src="${
                blog.profile_image
              }" alt="" />
              <div class="pl-5">
                <p class="font-bold">${blog.author.name}</p>
                <p class="text-gray-400">${
                  blog.author.designation ? blog.author.designation : "Unknown"
                }</p>
              </div>
            </div>
          </div>
        </div>
  `;
    latestPosts.appendChild(blogCard);
  });
};

blogCard();

// inpute field
const handleSearch = async () => {
  const input = document.getElementById("input").value;
  const res = await fetch(
    `https://openapi.programming-hero.com/api/retro-forum/posts?category=${input}`
  );
  const data = await res.json();
  console.log(data.posts);
  displayShow(data.posts);
};

```
