# safex-blockchain-explorer-docker
Running Safex Blockchain Explorer using Docker

Running this docker compose will run the Safex Blockchain Explorer and expose it on port 8000.
When the images dont exist yet (on first run) it will compile the <a href="https://github.com/safex/safexcore" target="_blank">Safex Core</a> and the <a href="https://github.com/safex/safex-blockchain-explorer" target="_blank">Safex Blockchain Explorer</a>.<br>The core <i>daemon</i> and the <i>explorer</i> run separate containers.<br><br>

The styling can be changed in the <i><b>styling</b></i> folder. These folders are served by the NGINX container. (<i>images</i>, <i>css</i>, <i>favicon</i> are mounted locations and can be changed during runtime)<br><br>


Running the daemon will sync it with the network. If you already have a synced database, then change the location in the <i><b>docker-compose.yml</b></i> file <u>twice</u> (line 14 and 29)! Change <i><b>/home/.safex</i></b> into te location where your <i><b>.safex</i></b> folder is, if it is not at this location:
<br>
<code>
volumes:<br>
      - <i><b>/home/.safex</i></b>:/home/docker/.safex
</code>

<h1>Running the explorer</h1>
<ul>
<li>install docker</li>
<li>download or clone this repo</li>
<li>navigate into the folder</li>
<li>run from a terminal: <code>$ docker-compose up</code></li>
<li>open the explorer at <code>http://localhost:8000</code></li>
</ul>
<br>
* running the command as sudo might be required depending on your priveliges<br>
* newer versions of compose are ran as <code>$ docker compose up</code> (without a dash)<br>
* compiling at first run might take a while<br>
* synchronizing a new daemon might take a while<br>
<br><br>
To exit:
<ul>
<li>press CTRL + C in the terminal</li>
<li>run from a terminal: <code>$ docker-compose down</code> to remove everything from docker</li>
</ul>
<br>

<h1>Using port 80</h1>
If you want to expose the Explorer on port 80 (for example to host on a webserver) then:<br>
Change portmapping in the <i><b>docker-compose.yml</b></i> file on line 44 from <i><b>8000</b></i>:8000 to <i><b>80</b></i>:8000
<br><br>

<h1>Example Installing Docker & Runing the Explorer(i.e. on a VPS)</h1>
<br>

<code>$ sudo apt update</code><br>
<code>$ sudo apt install snapd</code><br>
<code>$ sudo snap install docker</code><br>
<code>$ docker compose up</code> (from the downloaded/cloned projects folder)<br>
<br>

