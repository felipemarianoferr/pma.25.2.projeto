## Repositórios:

1. **[Account Service](https://github.com/felipemarianoferr/pma252.account-service)**
2. **[Auth Service](https://github.com/felipemarianoferr/pma252.auth-service)**
3. **[Gateway Service](https://github.com/felipemarianoferr/pma252.gateway-service)**
4. **[Product Service](https://github.com/felipemarianoferr/pma.25.2.product-service)**
5. **[Order Service](https://github.com/felipemarianoferr/pma.25.2.order-service)**

### Kubernetes Configurations

=== "Account Service"
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: account
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: account
      template:
        metadata:
          labels:
            app: account
        spec:
          containers:
            - name: account
              image: felipemf2/account:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
              resources:
                requests:
                  memory: "200Mi"
                  cpu: "50m"
                limits:
                  memory: "300Mi"
                  cpu: "200m"

    ---

    apiVersion: v1
    kind: Service
    metadata:
      name: account
      labels:
        app: account
    spec:
      type: LoadBalancer
      ports:
        - port: 80
          protocol: TCP
          targetPort: 8080

      selector:
        app: account
    ```

=== "Auth Service"
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: auth
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: auth
      template:
        metadata:
          labels:
            app: auth
        spec:
          containers:
            - name: auth
              image: felipemf2/auth:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
              env:
                - name: JWT_SECRET_KEY
                  valueFrom:
                    secretKeyRef:
                      name: jwt-secrets
                      key: JWT_SECRET_KEY
              resources:
                requests:
                  memory: "200Mi"
                  cpu: "50m"
                limits:
                  memory: "300Mi"
                  cpu: "200m"

    ---

    apiVersion: v1
    kind: Service
    metadata:
      name: auth
      labels:
        app: auth
    spec:
      type: LoadBalancer
      ports:
        - port: 80
          protocol: TCP
          targetPort: 8080

      selector:
        app: auth
    ```

=== "Gateway Service"
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: gateway
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: gateway
      template:
        metadata:
          labels:
            app: gateway
        spec:
          containers:
            - name: gateway
              image: felipemf2/gateway:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
              resources:
                requests:
                  memory: "200Mi"
                  cpu: "50m"
                limits:
                  memory: "300Mi"
                  cpu: "200m"

    ---

    apiVersion: v1
    kind: Service
    metadata:
      name: gateway
      labels:
        app: gateway
    spec:
      type: LoadBalancer
      ports:
        - port: 80
          protocol: TCP
          targetPort: 8080

      selector:
        app: gateway
    ```

=== "Product Service"
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: product
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: product
      template:
        metadata:
          labels:
            app: product
        spec:
          containers:
            - name: product
              image: felipemf2/product:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
              resources:
                requests:
                  memory: "200Mi"
                  cpu: "50m"
                limits:
                  memory: "300Mi"
                  cpu: "200m"

    ---

    apiVersion: v1
    kind: Service
    metadata:
      name: product
      labels:
        app: product
    spec:
      type: LoadBalancer
      ports:
        - port: 80
          protocol: TCP
          targetPort: 8080

      selector:
        app: product
    ```

=== "Order Service"
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: order
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: order
      template:
        metadata:
          labels:
            app: order
        spec:
          containers:
            - name: order
              image: felipemf2/order:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
              resources:
                requests:
                  memory: "200Mi"
                  cpu: "50m"
                limits:
                  memory: "300Mi"
                  cpu: "200m"

    ---

    apiVersion: v1
    kind: Service
    metadata:
      name: order
      labels:
        app: order
    spec:
      type: LoadBalancer
      ports:
        - port: 80
          protocol: TCP
          targetPort: 8080

      selector:
        app: order
    ```

![MiniKube](kube.png)