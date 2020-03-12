# github-actions-demo

[GitHub Actions 入門教程](http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)  

[Creating a personal access token for the command line](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)

Settings/Secrets 用的是 `ACCESS_TOKEN`。如果你不用這個名字，後面腳本裡的變量名也要跟著改。

package.json

```js
"homepage": "https://jacobhsu.github.io/github-actions-demo",
```

.github/workflows

 action：JamesIves/[github-pages-deploy-action](https://github.com/marketplace/actions/deploy-to-github-pages)  

```yml
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false

      - name: Build and Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@releases/v3
        with:
          ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
          BRANCH: gh-pages # The branch the action should deploy to.
          FOLDER: build # The folder the action should deploy.

```

1. 整個流程在master分支發生push事件時觸發。 
2. 只有一個job，運行在虛擬機環境ubuntu-latest。
3. 第一步是獲取源碼，使用的 action 是actions/checkout。
4. 第二步是構建和部署，使用的 action 是JamesIves/github-pages-deploy-action。
5. 第二步需要四個環境變量，分別為 GitHub 密鑰、發佈分支、構建成果所在目錄、構建腳本。其中，只有 GitHub 密鑰是秘密變量，需要寫在雙括號裡面，其他三個都可以直接寫在文件裡。

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

GitHub 發現了 workflow 文件以後，就會自動運行。你可以在網站上實時查看運行日誌，日誌默認保存30天。  
等到 workflow 運行結束，訪問 GitHub Page，會看到構建成果已經發上網了。
以後，每次修改後推送源碼，GitHub Actions 都會自動運行，將構建產物發佈到網頁。  

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `yarn build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
