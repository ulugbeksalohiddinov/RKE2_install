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
---------------------------------------------------------------------------------------------------
