#My Gulp Setup

```

var  	gulp = require ('gulp')
	uglify = require('gulp-uglify')
	sass = require('gulp-ruby-sass')
	plumber = require('gulp-plumber')
	concat = require('gulp-concat')
	imagemin = require('gulp-imagemin')
	prefix = require('gulp-autoprefixer');

// Minification of Javascript file
// Uglifies 
gulp.task('scripts', function(){
	gulp.src('js/*.js')
	.pipe(plumber() )
	.pipe(uglify()) /*uglify*/
	.pipe(gulp.dest('build/js'))
	// .pipe(livereload());
	
	// .pipe(connect.reload());
});

// Sass
gulp.task('styles', function() {
    return sass('sass/', {
	     style: 'expanded' 
	 })
    		.pipe( plumber() )
    		.pipe(prefix('last 2 versions'))
	    	.pipe(concat('style.css'))
	        	.pipe(gulp.dest('./'))
	       	// .pipe(livereload());
	    	// .pipe(connect.reload());
});

// Image task
gulp.task('image', function(){
	return gulp.src('images/*')
	.pipe(imagemin())
	.pipe(gulp.dest('build/img'));
});

// Watch task
/*Looks for a change */
gulp.task('watch', function(){ /*this is a build in watch method*/
	gulp.watch('js/*.js',  ['scripts']); /*watch the path and do scripts task*/ 
	gulp.watch('sass/*.scss',  ['styles']);
});


gulp.task('default', ['scripts',  'styles', 'image', 'watch' ]);
```