# demo-1

主要思路：回退保存回退的数据，前进时把保存的数据再拿出来，实现回退前进

如果在回退的途中新加入数据，则删除回退保存的数据，保证数据是没有分支只有一条主线

难点：因为watch是异步的，如果先改变n的值


## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
