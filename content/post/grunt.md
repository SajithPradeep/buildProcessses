+++
Categories = []
Tags = []
title = "Grunt"
draft = false
+++

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/androidstudio.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

<p class="custom-heading"> What is Grunt? </p>
<p>Grunt has made web development more enjoyable. By automating repetitive tasks, it has allowed web developers to focus on building features rather than copying, compiling, and configuring.
Here are some tips and best practices to get a better Gruntfile. </p>

<p class="custom-sub-heading"> Important files in any repo are as follows : </p>
<p><b>•	bower_components</b> – By default, Bower will install all its packages in this folder. You can configure it to place the packages in a specific folder by creating a “.bowerrc” file and adding a few configuration options there.</p>
<p><b>•	node_modules </b>– This is where NPM will store all its packages needed for the project.</p><p>
<p><b>•	.gitignore </b>– This file contains a list of patterns that Git will ignore by default. It helps to eliminate the chance of adding unnecessary files to the source repository.</p>
<p><b>•	bower.json</b> – This file contains some basic information and configuration for Bower. It essentially serves as a manifest file that tells the program which packages this project depends on. When you run “bower install,” it will look for this file and get the list of packages to download from there.</p>
<p><b>•	Gruntfile.js</b> – This file will contain all the Grunt.js tasks and configurations.</p>
<p><b>•	index.html</b> – The app’s main page.</p>
<p><b>•	package.json </b>– This is similar to the bower.json file, but for NPM.
</p>

<p class="custom-sub-heading">Load all grunt tasks with one line of code </p>
<p>Forget to add the classic loadNpmTask when you add a new plugin to use in your Gruntfile. It results in a unnecessary maintenance.</p>
<pre>
<code>
  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-browser-sync');
  grunt.loadNpmTasks('grunt-contrib-jasmine');
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-coffee');
</pre>
</code>

<p>There are two options to get that. The first is to the code above to that:</p>
<pre>
<code>
npm install --save-dev load-grunt-tasks
require('load-grunt-tasks')(grunt);
</pre>
</code>

<p>The other one is to use the matchdep node module which reads your package.json file and extracts all of the dependencies that match a specified string.
First, we have to install the module, and then, put this code into your gruntfile.</p>
<pre>
<code>
npm install --save-dev matchdep
require('matchdep').filterDev('grunt-*').forEach(grunt.loadNpmTasks);  //In your Gruntfile
</pre>
</code>

<p class="custom-sub-heading">Create alias to install plugins</p>
<p>Here is a gist with the two functions we can use to install plugins using aliases: Gist</p>
<pre>
<code>
function gi() {
  npm install --save-dev grunt-"$@"
}
function gci() {
  npm install --save-dev grunt-contrib-"$@"
}
gci watch
gi concurrent
</pre>
</code>

<p class="custom-sub-heading">Don't forget the debugging and verbose mode</p>
<p>It's normal to have errors in the middle of our Grunt configuration. In most cases, run a task with -v flag to get extended logging. For example:</p>
<pre>
<code>
grunt watch -v
</pre>
</code>
<p>if you need to look further into debugging a task by seeing a stack trace, you can also set the --stack flag.</p>
<pre>
<code>
grunt watch --stack
</code>
</pre>

<p class="custom-sub-heading">Use variables in your configuration</p>
<p>In Grunt it's important to declare variables for a better code and understanding.
For example, In my case, I always declare variables to define the paths of my project.
A little example is here, where I define variables to improve my Gruntfile configuration, and, of course, remove duplicate values using variables.
</p>
<pre>
<code>
var globalConfig = {
  baseSass: 'assets/sass',
  baseStyles: 'assets/css'
};
grunt.initConfig({
  globalConfig: globalConfig,
  sass: {
    applyStyle: {
      options: {
        style: 'compressed'
      },
      files: {
        '<%= globalConfig.baseStyles %>style.css': '<%= globalConfig.baseSass %>style.scss'
      }
    },
  }
});
</pre>
</code>

<p class="custom-sub-heading">Create a good watch task configuration</p>
<p>Grunt watch is essential for a good development workflow. Don't worry if you spend hours in it's configuration. In my opinion it's very important.
Use targets for separate to spread your tasks. For example it's no necessary to call sass task if a coffescript file is changed.
</p>
<pre>
<code>
watch: {
      options: {
        interrupt: true
      },
      styles: {
        files: ['**/*.scss'],
        tasks: ['sass:applyStyle']
      },
      test: {
        files: '**/*.coffee',
        tasks: ['jasmine']
      },
      lint: {
        files: '**/*.js',
        tasks: ['jshint']
      }
    }
</pre>
</code>
