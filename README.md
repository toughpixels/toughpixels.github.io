# [Tough Pixels Tips](https://toughpixels.com/)
Tips articles about various programming, content creation, and general livability articles.

## Usage

Install by cloning, then running `hugo server` in the directory.

Make a new Tip by running `hugo new tips/this-tip-is-about-something-awesome`.

## Deploying

The `docs` directory master branch of this project is deployed. Don't edit this if you don't want to deploy your code. 

To deploy your code, first push the changes you've made to the Hugo project, then run:
```
rm -rf docs
hugo --minify
git add .
git commit -am "MY CHANGE"
git push
```
