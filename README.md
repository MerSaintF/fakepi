[spanish](https://github.com/SofiDevO/alurageek-API/tree/spanish)

## Deploy JSON Server to Vercel

A template for deploying [JSON Server](https://github.com/typicode/json-server) on [Vercel](https://vercel.com), allowing you to run a fake REST API online 🐣!

Demo from this repository:
https://alurageek-api.vercel.app/

### How to use (resume)

1. Click "**Use this template**" or clone this repository.
2. Update or use the default [`db.json`](./db.json) in the repository.
3. Sign up or log in to [Vercel](https://vercel.com).
4. From the Vercel dashboard, click "**+ New Project**" and then "**Import**" your repository.
5. On the "**Configure Project**" screen, leave everything as default and click "**Deploy**".
6. Wait until deployment is complete, and your custom JSON server will be ready to serve!

## Default `db.json`

```json
{
  "products": [
    {
      "id": "79393f24-3bbb-401b-9a94-67eccc8f2197",
      "productName": "Stitch",
      "img": "https://funkimia.com/wp-content/uploads/2024/02/funko-pop-monster-stitch.webp",
      "price": 300
    },
    {
      "id": "bdc7c941-7dd8-46b9-a0f3-7c1c62c537c3",
      "productName": "Rapunzel",
      "img": "https://funkimia.com/wp-content/uploads/2022/12/funko-pop-rapunzel.webp",
      "price": 550
    },
    {
      "id": "47c93f01-0119-4586-a353-0d0e2a3a167e",
      "productName": "Meilin Lee",
      "img": "https://funkimia.com/wp-content/uploads/2022/12/funko-pop-meilin-lee.webp",
      "price": 329
    },
    {
      "id": "09fc5f6f-748a-407a-90dd-ed9f4f982bd3",
      "productName": "Mike Wazowski",
      "img": "https://funkimia.com/wp-content/uploads/2022/02/funko-pop-mike-wazowski.webp",
      "price": "290"
    },
    {
      "id": "c718f481-8085-4176-a7be-5b5377602e65",
      "productName": "Pato Donald",
      "img": "https://funkimia.com/wp-content/uploads/2021/12/funko-pop-donald-duck-christmas.jpg",
      "price": "290"
    },
    {
      "id": "2da9f369-9690-42fa-8f2a-b1f02bfa0783",
      "productName": "Maribel Madrigal",
      "img": "https://funkimia.com/wp-content/uploads/2022/02/funko-pop-mirabel.webp",
      "price": "290"
    },
    {
      "id": "1f828bd8-feb4-4f79-b8dc-ef30472a32d3",
      "productName": "Vanellope",
      "img": "https://funkimia.com/wp-content/uploads/2022/02/funko-pop-vanellope.webp",
      "price": "600"
    },
    {
      "id": "fa7403f9-4839-420c-8219-d93172b70686",
      "productName": "Yeti",
      "img": "https://funkimia.com/wp-content/uploads/2022/02/funko-pop-yeti.jpg",
      "price": "270"
    },
    {
      "id": "15aa61f4-ab74-4fdd-9457-d645c63ddf22",
      "productName": "Princesa Leia",
      "img": "https://m.media-amazon.com/images/I/61p1tVCll0L._AC_SY450_.jpg",
      "price": "500"
    }
  ]
}
```

## Build It Yourself

If you'd like to create the project from scratch, I have a [YouTube video Tutorial (Spanish) that guides you through deploying your own fake API with db-json and Vercel.](https://www.youtube.com/channel/UC36_js-krsAHAEAWpEDhHtw)

### Step 1

Create a new repository, for example, **alurageek-API**. Then clone that empty repository.

### Step 2

You need to run the npm init command:

```
npm init -y
```

This will generate a **package.json**. Now, what you need to do is change these lines:

Change this line:

```
 "main": "index.js",
```

To this:

```
  "main": "api/server.js",
```

And this:

```
"test": "echo \"Error: no test specified\" && exit 1"
```

To this:

```
"start": "node api/server.js"
```

### Step 3

Now it's time to run the command:

```
npm install json-server cors
```

![Alt text](image.png)

You'll see that both **cors** and **_json-server_** have been added to the package.json.

### Step 4

Run the command:

```
npm install json-server
```

Add the **_.gitignore_** file and add **_node_modules_**.

### Step 5

Create a **_db.json_** file and add your own data.

Additionally, you'll need to add a new [Folder called **_api_**](./api/) and, inside it, this [**server.js**](./api/server.js) file:

```javascript
// See https://github.com/typicode/json-server#module
const jsonServer = require("json-server");
const server = jsonServer.create();
const router = jsonServer.router("db.json");
const middlewares = jsonServer.defaults();

server.use(middlewares);
// Add this before server.use(router)
server.use(
  jsonServer.rewriter({
    "/api/*": "/$1",
    "/product/:resource/:id/show": "/:resource/:id",
  })
);
server.use(router);
server.listen(3000, () => {
  console.log("JSON Server is running");
});

// Export the Server API
module.exports = server;
```

### Step 6

Create a new file named [**_vercel.json_**](./vercel.json)

```json
{
  "functions": {
    "api/server.js": {
      "memory": 1024,
      "includeFiles": "db.json"
    }
  },
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "api/server.js"
    }
  ]
}
```

# Don't forget to commit & push your changes 🐣

Go to your Vercel account, connect a new project with your repository, and deploy it💙

## You must be patient

It could take a couple of minutes to finally work. ⏰🥹
