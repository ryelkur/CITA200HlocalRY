If you are on the CITA network you can `git clone`, `git pull` and `git push` between your laptop and a CITA server directly like `git XXX USERNAME@SERVER.cita.utoronto.ca`.

However, CITA servers are not open to the Internet. To access a repo on a CITA server you need to set up an SSH proxy. The following instruction works on Mac and Linux.

Add the following to `~/.ssh/config` **on your home computer/laptop**, substituting in your username. If `config` file doesn't exist just create one.

```{.bash}
ControlMaster auto
 
Host gw*.cita.utoronto.ca
    ProxyCommand none
 
Host *.cita.utoronto.ca
    ProxyCommand ssh <username>@gw.cita.utoronto.ca nc %h %p
```

With this you will be able to run the same git command. For example [[Lecture1---Activity-1]]

`git clone USERNAME@trinity.cita.utoronto.ca:repos/gauss2d.git`

Note that you will prompt you password twice, once from your computer to gateway, again from gateway to the server.