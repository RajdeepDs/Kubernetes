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

<h3>HOSTPATH</h3>
<p>A HostPath colume mounts a file or directory from nodes file system into the Pod.</p>
The HostPath can be used as --
<ul>
<li>Running container needs access to the docker internals, so var/lib can be mounted.</li>
<li>'C' advisor can be run on a container by mounting /zish of a node</li>
<li>Pod checks wether the directory exits or not and if yes, then only the pod will run</li>
</ul>
These both EMPTYDIR & HOSTPATH can be used as saving the data.

    #YAML
    Containers:
    -image: alpine
     name: hostpath-container
     command: ['sh','-c','sleep 3000']
     VolumeMounts:
     -mountPath: /demo
      name: hp-volume
    volumes:
    -name: hp-volume
     hostPath: 
        path: /data
        type: DirectoryOrCreate

