<h2 align="middle">KUBERNETES VOLUMES</h2>
<h3>EMPTYDIR</h3>
<p>It gets created as soon as the Pods assigned to the Nodes. It stays throughout the lifespan of the Pod and as soon as the Pod deleted, the EMPTYDIR is also removed.<br></p>
The EMPTYDIR can be used such as --
<ul>
<li>Scratch Space</li>
<li>Sorting Algorithm</li>
<li>CheckPointing in long competition in the ram.</li>
</ul>
<p>The EMPTYDIR either can be based on the node disk attached to the Node or if you specify the EMPTYDIR "medium" instead of "{}" the it will create a TMPFS and use the ram as the volume</p>

    #YAML
    Containers:
        -image: alpine
         name: emptydir-container
         command : ['sh','-c','sleep 3000']
    VolumeMounts:
        -mountPath: /demo
         name: test-vol
    Volumes:
        -name: test-vol
         EmptyDir: {}
