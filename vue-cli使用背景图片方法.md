# vue-cli使用背景图片方法

如果发现背景图片在npm run build之后无法实现
 
在build/utils.js 目录下找到
 
function generateLoaders(loader, loaderOptions) {
    const loaders = options.usePostCSS ? [cssLoader, postcssLoader] : [cssLoader]
    if (loader) {
        loaders.push({
            loader: loader + '-loader',
            options: Object.assign({}, loaderOptions, {
                sourceMap: options.sourceMap
            })
        })
    }

    // Extract CSS when that option is specified
    // (which is the case during production build)
    if (options.extract) {
        return ExtractTextPlugin.extract({
            use: loaders,
            publicPath: '../../', // 此为需要添加的！！！！！！！！！！！！！！！！！！！！！！！！
            fallback: 'vue-style-loader'
        })
    } else {
        return ['vue-style-loader'].concat(loaders)
    }
}

#### date 2018.5.24