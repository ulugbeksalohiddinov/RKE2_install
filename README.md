# RKE2_install

**Master install RKE2**

    curl -sfL https://get.rke2.io | sh -
    systemctl enable rke2-server.service
    systemctl start rke2-server.service
    journalctl -u rke2-server -f

    /var/lib/rancher/rke2/bin/kubectl get nodes

    ln -s /var/lib/rancher/rke2/bin/kubectl /usr/local/bin/kubectl  # kubectlni global qilish

    mkdir -p ~/.kube
    sudo cp /etc/rancher/rke2/rke2.yaml ~/.kube/config
    sudo chown $USER:$USER ~/.kube/config
    kubectl get nodes


**Worker install RKE2**

        curl -sfL https://get.rke2.io | INSTALL_RKE2_TYPE="agent" sh -
        systemctl enable rke2-agent.service

#Bu qadamlar RKE2 clusterga yangi node qo‘shish (join qilish) uchun ishlatiladi.
Ya’ni siz worker yoki yana bir server node ni mavjud master clusterga ulayapsiz.

        mkdir -p /etc/rancher/rke2/ #Bu yerda RKE2 konfiguratsiya fayllari saqlanadi.
        nano /etc/rancher/rke2/config.yaml 

        server: https://<server>:9345 # masterni ip addresi ko'rsatiladi
        token: <token from server node> # masterdan tokenolinib shu yerga qo'yiladi. cat /var/lib/rancher/rke2/server/node-token

        Misol:
        server: https://172.26.47.50:9345
        token: K108cdbbf226627133fc44f448e54168a2a306a15fd87a67e2b8cc50f8977981666::server:46813fc216b7e13

        systemctl start rke2-agent.service
        journalctl -u rke2-agent -f
