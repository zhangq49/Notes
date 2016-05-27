# node.js包教不包会
*Thursday, April 28,  2016*
## 0. 搭建node.js开发环境
**nvm（Node Version Manager）** 或 ** n** 都可以作为**node**版本管理的工具
nvm工具托管地址： [https://github.com/creationix/nvm]()
nvm命令行安装
	curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
或者
	wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
## 1. 一个最简单的express应用
### 框架Express
[http://expressjs.com/ ]()
> Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.
	// 这句的意思就是引入 express 模块，并将它赋予 express 这个变量等待使用。
	var express = require('express');
	// 调用 express 实例，它是一个函数，不带参数调用时，会返回一个 express 实例，将这个变量赋予 app 变量。
	var app = express();
	
	// app 本身有很多方法，其中包括最常用的 get、post、put/patch、delete，在这里我们调用其中的 get 方法，为我们的 `/` 路径指定一个 handler 函数。
	// 这个 handler 函数会接收 req 和 res 两个对象，他们分别是请求的 request 和 response。
	// request 中包含了浏览器传来的各种信息，比如 query 啊，body 啊，headers 啊之类的，都可以通过 req 对象访问到。
	// res 对象，我们一般不从里面取信息，而是通过它来定制我们向浏览器输出的信息，比如 header 信息，比如想要向浏览器输出的内容。这里我们调用了它的 #send 方法，向浏览器输出一个字符串。
	app.get('/', function (req, res) {
	  res.send('Hello World');
	});
	
	// 定义好我们 app 的行为之后，让它监听本地的 3000 端口。这里的第二个函数是个回调函数，会在 listen 动作成功后执行，我们这里执行了一个命令行输出操作，告诉我们监听动作已完成。
	app.listen(3000, function () {
	  console.log('app is listening at port 3000');
	});
## 2.  学习使用外部模块
安装模块
	$ npm install express utility --save
建立一个 lesson2 项目，在其中编写代码。当在浏览器中访问 http://localhost:3000/?q=alsotang 时，输出 alsotang 的 md5 值，即bdd5e57b5c0040f9dc23d430846e68a3。
	// 引入依赖
	var express = require('express');
	var utility = require('utility');
	
	// 建立 express 实例
	var app = express();
	
	app.get('/', function (req, res) {
	  // 从 req.query 中取出我们的 q 参数。
	  // 如果是 post 传来的 body 数据，则是在 req.body 里面，不过 express 默认不处理 body 中的信息，需要引入 https://github.com/expressjs/body-parser 这个中间件才会处理，这个后面会讲到。
	  // 如果分不清什么是 query，什么是 body 的话，那就需要补一下 http 的知识了
	  var q = req.query.q;
	
	  // 调用 utility.md5 方法，得到 md5 之后的值
	  // 之所以使用 utility 这个库来生成 md5 值，其实只是习惯问题。每个人都有自己习惯的技术堆栈，
	  // 我刚入职阿里的时候跟着苏千和朴灵混，所以也混到了不少他们的技术堆栈，仅此而已。
	  // utility 的 github 地址：https://github.com/node-modules/utility
	  // 里面定义了很多常用且比较杂的辅助方法，可以去看看
	  var md5Value = utility.md5(q);
	
	  res.send(md5Value);
	});
	
	app.listen(3000, function (req, res) {
	  console.log('app is running at port 3000');
	});
## 3. 使用superagent与cheerio完成简单爬虫
### **superagent** — 轻量级的HTTP异步请求模块
`链式调用`
`官网地址`：[http://visionmedia.github.io/superagent/]()
> Super Agent is light-weight progressive ajax API crafted for flexibility, readability, and a low learning curve after being frustrated with many of the existing request APIs. It also works with Node.js!
	request
	   .post('/api/pet')
	   .send({ name: 'Manny', species: 'cat' })
	   .set('X-API-Key', 'foobar')
	   .set('Accept', 'application/json')
	   .end(function(err, res){
	     if (err || !res.ok) {
	       alert('Oh no! error');
	     } else {
	       alert('yay got ' + JSON.stringify(res.body));
	     }
	   });
### ** cheerio** — 服务端的核心jQuery实现
`模块地址`：[https://github.com/cheeriojs/cheerio][4] 
> Fast, flexible, and lean implementation of core jQuery designed specifically for the server.
	var cheerio = require('cheerio'),
	    $ = cheerio.load('<h2 class="title">Hello world</h2>');
	
	$('h2.title').text('Hello there!');
	$('h2').addClass('welcome');
	
	$.html();
	//=> <h2 class="title welcome">Hello there!</h2>
### `爬虫程序核心逻辑`
	app.get('/', function (req, res, next) {
	  // 用 superagent 去抓取 https://cnodejs.org/ 的内容
	  superagent.get('https://cnodejs.org/')
	    .end(function (err, sres) {
	      // 常规的错误处理
	      if (err) {
	        return next(err);
	      }
	      // sres.text 里面存储着网页的 html 内容，将它传给 cheerio.load 之后
	      // 就可以得到一个实现了 jquery 接口的变量，我们习惯性地将它命名为 `$`
	      // 剩下就都是 jquery 的内容了
	      var $ = cheerio.load(sres.text);
	      var items = [];
	      $('#topic_list .topic_title').each(function (idx, element) {
	        var $element = $(element);
	        items.push({
	          title: $element.attr('title'),
	          href: $element.attr('href')
	        });
	      });
	
	      res.send(items);
	    });
	});
## 4. 使用eventproxy控制并发
### ** eventproxy** — 轻量级处理异步并发的工具
`模块地址`：[https://github.com/JacksonTian/eventproxy][5] 
> EventProxy 仅仅是一个很轻量的工具，但是能够带来一种事件式编程的思维变化。有几个特点：
> 1.    利用事件机制解耦复杂业务逻辑
> 2.    移除被广为诟病的深度callback嵌套问题
> 3.    将串行等待变成并行等待，提升多异步协作场景下的执行效率
> 4.    友好的Error handling
> 5.    无平台依赖，适合前后端，能用于浏览器和Node.js
> 6.    兼容CMD，AMD以及CommonJS模块环境
`核心逻辑`
爬取帖子url
	var eventproxy = require('eventproxy');
	var superagent = require('superagent');
	var cheerio = require('cheerio');
	// url 模块是 Node.js 标准库里面的
	// http://nodejs.org/api/url.html
	var url = require('url');
	
	var cnodeUrl = 'https://cnodejs.org/';
	
	superagent.get(cnodeUrl)
	  .end(function (err, res) {
	    if (err) {
	      return console.error(err);
	    }
	    var topicUrls = [];
	    var $ = cheerio.load(res.text);
	    // 获取首页所有的链接
	    $('#topic_list .topic_title').each(function (idx, element) {
	      var $element = $(element);
	      // $element.attr('href') 本来的样子是 /topic/542acd7d5d28233425538b04
	      // 我们用 url.resolve 来自动推断出完整 url，变成
	      // https://cnodejs.org/topic/542acd7d5d28233425538b04 的形式
	      // 具体请看 http://nodejs.org/api/url.html#url_url_resolve_from_to 的示例
	      var href = url.resolve(cnodeUrl, $element.attr('href'));
	      topicUrls.push(href);
	    });
	
	    console.log(topicUrls);
	  });
爬取各帖子url下的首条评论， 异步并发控制
	// 得到 topicUrls 之后
	
	// 得到一个 eventproxy 的实例
	var ep = new eventproxy();
	
	// 命令 ep 重复监听 topicUrls.length 次（在这里也就是 40 次） `topic_html` 事件再行动
	ep.after('topic_html', topicUrls.length, function (topics) {
	  // topics 是个数组，包含了 40 次 ep.emit('topic_html', pair) 中的那 40 个 pair
	
	  // 开始行动
	  topics = topics.map(function (topicPair) {
	    // 接下来都是 jquery 的用法了
	    var topicUrl = topicPair[0];
	    var topicHtml = topicPair[1];
	    var $ = cheerio.load(topicHtml);
	    return ({
	      title: $('.topic_full_title').text().trim(),
	      href: topicUrl,
	      comment1: $('.reply_content').eq(0).text().trim(),
	    });
	  });
	
	  console.log('final:');
	  console.log(topics);
	});
	
	topicUrls.forEach(function (topicUrl) {
	  superagent.get(topicUrl)
	    .end(function (err, res) {
	      console.log('fetch ' + topicUrl + ' successful');
	      ep.emit('topic_html', [topicUrl, res.text]);
	    });
	});
## 5. 使用async控制并发
### **async** — 强大功能的异步js工具模块
`模块地址`：[https://github.com/caolan/async][6]
`模块演示地址`: [https://github.com/alsotang/async\_demo][7]
> Async is a utility module which provides straight-forward, powerful functions for working with asynchronous JavaScript. Although originally designed for use with Node.js and installable via npm install --save async, it can also be used directly in the browser.
> Async is also installable via:
> •   `bower: bower install async`
> •   `component: component install caolan/async`
> •   `jam: jam install async`
> Async provides around 70 functions that include the usual 'functional' suspects (map, reduce, filter, each…) as well as some common patterns for asynchronous control flow (parallel, series, waterfall…). All these functions assume you follow the Node.js convention of providing a single callback as the last argument of your asynchronous function -- a callback which expects an Error as its first argument -- and calling the callback once.
`Quick Example`
	async.map(['file1','file2','file3'], fs.stat, function(err, results){
	    // results is now an array of stats for each file
	});
	
	async.filter(['file1','file2','file3'], function(filePath, callback) {
	  fs.access(filePath, function(err) {
	    callback(null, !err)
	  });
	}, function(err, results){
	    // results now equals an array of the existing files
	});
	
	async.parallel([
	    function(){ ... },
	    function(){ ... }
	], callback);
	
	async.series([
	    function(){ ... },
	    function(){ ... }
	]);
#### 核心逻辑
首先，我们伪造一个 fetchUrl(url, callback) 函数，这个函数的作用就是，当你通过
	fetchUrl('http://www.baidu.com', function (err, content) {
	  // do something with `content`
	});
调用它时，它会返回 `http://www.baidu.com` 的页面内容回来。
当然，我们这里的返回内容是假的，返回延时是随机的。并且在它被调用时，会告诉你它现在一共被多少个地方并发调用着。
	// 并发连接数的计数器
	var concurrencyCount = 0;
	var fetchUrl = function (url, callback) {
	  // delay 的值在 2000 以内，是个随机的整数
	  var delay = parseInt((Math.random() * 10000000) % 2000, 10);
	  concurrencyCount++;
	  console.log('现在的并发数是', concurrencyCount, '，正在抓取的是', url, '，耗时' + delay + '毫秒');
	  setTimeout(function () {
	    concurrencyCount--;
	    callback(null, url + ' html content');
	  }, delay);
	};
我们接着来伪造一组链接
	var urls = [];
	for(var i = 0; i < 30; i++) {
	  urls.push('http://datasource_' + i);
	}
接着，我们使用 `async.mapLimit` 来并发抓取，并获取结果。
	async.mapLimit(urls, 5, function (url, callback) {
	  fetchUrl(url, callback);
	}, function (err, result) {
	  console.log('final:');
	  console.log(result);
	});
`运行结果`
![][image-1]
## 6. 后端测试用例： mocha, should, istanbul
### **mocha** — JavaScript测试框架(前后端通吃)
`官网`：[http://mochajs.org/][8]
> Mocha is a feature-rich JavaScript test framework running on Node.js and in the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases. Hosted on GitHub.

	var assert = require('chai').assert;
	describe('Array', function() {
	  describe('#indexOf()', function () {
	    it('should return -1 when the value is not present', function () {
	      assert.equal(-1, [1,2,3].indexOf(5));
	      assert.equal(-1, [1,2,3].indexOf(0));
	    });
	  });
	});
### **should** — 断言库
`模块地址`: [https://github.com/tj/should.js][9]
> should is an expressive, readable, test framework agnostic, assertion library. Main goals of this library to be expressive andto be helpful. It keeps your test code clean, and your error messages helpful.
> It extends the Object.prototype with a single non-enumerable getter that allows you to express how that object should behave, also it returns itself when required with require.
	var should = require('should');
	
	var user = {
	    name: 'tj'
	  , pets: ['tobi', 'loki', 'jane', 'bandit']
	};
	
	user.should.have.property('name', 'tj');
	user.should.have.property('pets').with.lengthOf(4);
	
	// if the object was created with Object.create(null)
	// then it doesn't inherit `Object` and have the `should` getter
	// so you can do:
	
	should(user).have.property('name', 'tj');
	should(true).ok;
	
	someAsyncTask(foo, function(err, result){
	  should.not.exist(err);
	  should.exist(result);
	  result.bar.should.equal(foo);
	});

### **istanbul** — JS code coverage tool
`模块地址`: [https://github.com/gotwarlost/istanbul][10]
> Yet another JS code coverage tool that computes statement, line, function and branch coverage with module loader hooks to transparently add coverage when running tests. Supports all JS coverage use cases including unit tests, server side functional tests and browser tests. Built for scale.
### 使用**Makefile**进行配置
	test:
	  ./node_modules/.bin/mocha
	
	cov test-cov:
	  ./node_modules/.bin/istanbul cover _mocha
	
	.PHONY: test cov test-cov
## 7. 浏览器测试用例：mocha, chai, phantomjs
### **chai** — 全栈式断言库
`官网`：[http://chaijs.com/][11]
> Chai is a BDD(行为驱动开发) / TDD(测试驱动开发) assertion library for node and the browser that can be delightfully paired with any javascript testing framework.

### **phantomJS** — Full web stack No browser required
`官网`：[http://phantomjs.org/][12]
> PhantomJS is a headless WebKit scriptable with a JavaScript API. It has fast andnative support for various web standards: DOM handling, CSS selector, JSON, Canvas, and SVG.
	// Simple Javascript example
	
	console.log('Loading a web page');
	var page = require('webpage').create();
	var url = 'http://phantomjs.org/';
	page.open(url, function (status) {
	  //Page is loaded!
	  phantom.exit();
	});
搭建一个测试原型，用 mocha 自带的脚手架可以自动生成
	cd vendor            # 进入我们的项目文件夹
	npm i -g mocha       # 安装全局的 mocha 命令行工具
	mocha init .         # 生成脚手架
mocha就会自动帮我们生成一个简单的测试原型, 目录结构如下
	.
	├── index.html       # 这是前端单元测试的入口
	├── mocha.css
	├── mocha.js
	└── tests.js         # 我们的单元测试代码将在这里编写
mocha没有提供一个命令行的前端脚本测试环境(因为我们的脚本文件需要运行在浏览器环境中)，因此我们使用phanatomjs帮助我们搭建一个模拟环境。不重复制造轮子，这里直接使用mocha-phantomjs帮助我们在命令行运行测试。
	mocha-phantomjs index.html --ssl-protocol=any --ignore-ssl-errors=true
更进一步，可以直接在 package.json 的 scripts 中添加 
	"scripts": {
	  "test": "mocha-phantomjs index.html --ssl-protocol=any --ignore-ssl-errors=true"
	},
直接运行
	npm test
## 8. 测试用例：supertest
### **supertest** — Super-agent driven library for testing node.js HTTP servers using a fluent API(HTTP服务器测试工具)
> The motivation with this module is to provide a high-level abstraction for testing HTTP, while still allowing you to drop down to the lower-level API provided by super-agent.
	var request = require('supertest');
	var express = require('express');
	
	var app = express();
	
	app.get('/user', function(req, res) {
	  res.status(200).json({ name: 'tobi' });
	});
	
	request(app)
	  .get('/user')
	  .expect('Content-Type', /json/)
	  .expect('Content-Length', '15')
	  .expect(200)
	  .end(function(err, res) {
	    if (err) throw err;
	  });
### **nodemon** — 实时更新改动，不需重启服务的调试工具
`模块地址`：[https://github.com/remy/nodemon][13]
> nodemon does not require any changes to your code or method of development. nodemon simply wraps your node application and keeps an eye on any files that have changed. Remember that nodemon is a replacement wrapper for node, think of it as replacing the word "node" on the command line when you run your script.

Nodeclub 里面的测试使用的技术跟前面介绍的是一样的，should mocha supertest 那套，应该是很容易看懂的:
[https://github.com/cnodejs/nodeclub/blob/master/test/controllers/topic.test.js]()

## 9. 正则表达式

## 10. benchmark 怎么写
### ** benchmark** — A benchmarking library
`项目地址`：[https://github.com/bestiejs/benchmark.js][15]
`官网地址`：[https://benchmarkjs.com/][16]
> A robust benchmarking library that supports high-resolution timers & returns statistically significant results. As seen onjsPerf.
### **jsPerf** — 个基于JSLitmus的基准测试库（网站更新中）
> 在前端开发的过程中，掌握好浏览器的特性进行有针对性的性能调优是一项基本工作，jsperf.com是一个用来发布基于HTML的针对性能比较的测试用例的网站，你可以在jsPerf上在线填写和运行测试用例，得到浏览器运行测试用例的性能，学会利用jsPerf会让你的优化工作事半功倍。
> 比如，当我们想比较RegExp的test方法和String对象的indexOf方法查找字符串谁的速度更快的话，js代码在不同的浏览器，不同的操作系统环境运行的效率可能是不一样的，这就是为什么我们需要对其进行基准测试，在做基准测试方面，我们可以使用Benchmark.js和使用jsPerf（一个基于JSLitmus的基准测试库）。我们可以使用jsPerf来分享你的基准测试。
\`使用Benchmark.js和jsPerf分析代码性能
\`[https://segmentfault.com/a/1190000003486676][17]
### 内容
有一个字符串 var number = '100'，我们要将它转换成 Number 类型的 100。
目前有三个选项：+, parseInt, Number
主逻辑代码
	var Benchmark = require('benchmark');
	
	var suite = new Benchmark.Suite;
	
	var int1 = function(str) {
		return +str;
	};
	
	var int2 = function(str) {
		return parseInt(str, 10);
	};
	
	var int3 = function(str) {
		return Number(str);
	};
	
	var number = '100';
	// 添加测试
	suite
	.add('+', function() {
	  int1(number);
	})
	.add('parseInt', function() {
	  int2(number);
	})
	.add('Number', function () {
	  int3(number);
	})
	// 每个测试跑完后，输出信息
	.on('cycle', function(event) {
	  console.log(String(event.target));
	})
	.on('complete', function() {
	  console.log('Fastest is ' + this.filter('fastest').map('name'));
	})
	// 这里的 async 不是 mocha 测试那个 async 的意思，这个选项与它的时间计算有关，默认勾上就好了。
	.run({ 'async': true });

## 12. 线上部署：heroku
#### 什么是 heroku
heroku 是弄 ruby 的 paas 起家，现在支持多种语言环境，更甚的是它强大的 add-on 服务。
paas 平台相信大家都不陌生。Google 有 gae，国内新浪有 sae。paas 平台相对 vps 来说，不需要你配置服务器，不需要装数据库，也不需要理会负载均衡。这一切都可以在平台上直接获取。
你只要专注自己的业务，把应用的逻辑写好，然后发布上去，应用自然就上线了。数据库方面，如果你用 mysql，那么你可以从平台商那里得到一个 mysql 的地址、账号和密码，直接连接就能用。如果应用的流量增大，需要横向拓展，则只用去到 paas 平台的管理页面，增大服务器实例的数量即可，负载均衡会自动帮你完成。
### `Heroku` — a cloud platform
> Heroku is a cloud platform that lets companies build, deliver, monitor and scale apps — we're the fastest way to go from idea to URL, bypassing all those infrastructure headaches.
## 13. 持续集成平台：travis
### `Travis CI` — Test and Deploy with Confidence
> Easily sync your GitHub projects with Travis CI and you’ll be testing your code in minutes!
## 15. Mongodb 与 Mongoose 的使用
### Mongoldb
* hbase 和 redis 和 mongodb 和 couchdb 虽然都属于 nosql 的大范畴。但它们关注的领域是不一样的。hbase 是存海量数据的，redis 用来做缓存，而 mongodb 和 couchdb 则试图取代一些使用 mysql 的场景。
* 在 sql 中，我们的数据层级是：数据库（db） -\> 表（table） -\> 记录（record）-\> 字段；在 mongodb 中，数据的层级是：数据库 -\> collection -\> document -\> 字段。这四个概念可以对应得上。
### Mongoose
* mongoose 是个 odm。odm 的概念对应 sql 中的 orm。也就是 ruby on rails 中的 activerecord 那一层。orm 全称是 Object-Relational Mapping，对象关系映射；而 odm 是 Object-Document Mapping，对象文档映射。
* 它的作用就是，在程序代码中，定义一下数据库中的数据格式，然后取数据时通过它们，可以把数据库中的 document 映射成程序中的一个对象，这个对象有 .save .update 等一系列方法，和 .title .author 等一系列属性。在调用这些方法时，odm 会根据你调用时所用的条件，自动转换成相应的 mongodb shell 语句帮你发送出去。自然地，在程序中链式调用一个个的方法要比手写数据库操作语句具有更大的灵活性和便利性。




[4]:	https://github.com/cheeriojs/cheerio
[5]:	https://github.com/JacksonTian/eventproxy
[6]:	https://github.com/caolan/async "模块地址"
[7]:	https://github.com/alsotang/async_demo
[8]:	http://mochajs.org/
[9]:	https://github.com/tj/should.js
[10]:	https://github.com/gotwarlost/istanbul
[11]:	http://chaijs.com/
[12]:	http://phantomjs.org/
[13]:	https://github.com/remy/nodemon
[15]:	https://github.com/bestiejs/benchmark.js
[16]:	https://benchmarkjs.com/
[17]:	https://segmentfault.com/a/1190000003486676

[image-1]:	file:///.file/id=6571367.7226622