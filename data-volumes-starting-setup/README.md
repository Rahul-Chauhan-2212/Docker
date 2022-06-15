### Project: data-volumes-starting-setup

This app creates file with title name and content of file will be feedback.

<h5>docker build -t feedback-node .</h5>
<h5>docker run -p 3000:80 -d --name feedback-app --rm feedback-node</h5>

The file can be accessed with url
<a href="http://localhost:3000/feedback/titlewithsmallercase.txt"></a>

the file is created inside container but not in our local system. as soon as the container is removed then the files are also lost.</br>

Only VOLUME ["/app/feedback"] breaks the code so have to update the js code.</br>
But still only this does not solve our main issue.
