# kringles.org-staging
jekyll setup for kringles.org

# How to Test
bundle exec jekyll serve --host=0.0.0.0

# How to update prod
cd ../pkringle.github.io
git pull
cd ../kringles.org-staging
bundle exec jekyll build -d ../defunctknightsurfer.github.io/
cd ../pkringle.github.io
git add .
git commit -m "Something cool was done here"
git push origin master
