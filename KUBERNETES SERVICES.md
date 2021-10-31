<h2 align="middle">KUBERNETES SERVICES</h2>

<h4>Introduction to Services</h4>
<img src="Resources/SERVICES.png">
<h4>Let's spinup pod : </h4>

    kubectl get nodes
    kubectl get all 
    kubectl create ns [Namespace_Name]

    # Once the ns created, now we can deploy pod to ns

    kubectl apply -f [PodName] -n [Namespace_Name]
    kubectl get all -n [Namespace_Name]

    # To delete Pod

    kubectl delete pod [PodName] -n [Namespace_Name]

In Kubernetes we can use "reconsile"
To reconsile our resources. When our pod dies, we want a new pod spinup, So we use deployment.

    # To deploy deployment in namespace
    
    kubectl apply -f [Deployment_Name].yaml -n [Namespace_Name]

    # To see all information

    kubectl get all -n [Namespace_Name]

    # To delete Pod

    kubectl delete [Pod_Name] -n [Namespace_Name]

    When, we delete a existing pod, we see that a new pod created in place of deleted Pod.

    # To access specific pod

    kubectl port-forward [Pod_Name] -n [Namespace_Name] 8080:8080 <<- [PortNumber]

    Now, Open Browser and
    search "localhost:8080" <<-[PortNumber]

<p>When we are doing Port-forwarding, if the pod dies the link here is gonna be broken, and I won't able to access this pod anymore. And this is when the Kubernetes services coming, the service instead of port-forwarding, we will deploy a Kubernetes service and the Kubernetes service will basically specify, now we can connect to our deployment in that case if one of this pod dies and a new pod is spinup, I will be automatically forward to the other pod. And that Pod dies it will spinup Pod1 , it will automatically back to other pod itself. If both Pod alive, it will routed to any of the pod or the pod have least traffic.<br>
So, a Kubernetes Service basically allows us to connect to navigate to different Pod.</p>
<img src="Resources/DEPLOYMENT.png">
<hr>
<img src="Resources/APPLICATION.png">
<p>Lets Assume, we have FrontEnd, BackEnd and DataBase, all have three Pods with different EndPoints, simultaneously. If any of the Pod from FrontEnd dies, it will automatically creates another Pod with different EndPoint. So, we cannot assign the BackEnd to directly talk with these EndPoint, because the EndPoints are always changes. Insteads we will spinup services between those different sections of our Applications. In this case the services assigned a specific EndPoint. So, we can tell the BackEnd this is the service, that always communicate to. And these service allows us to communicate with deployment that have Pod in it.<p>
There are three different types of Kubernetes Services :
<ul>
<li>Cluster IP</li>
<li>NodePort</li>
<li>LoadBalancer</li>
<li>Headless Service</li>
</ul>
