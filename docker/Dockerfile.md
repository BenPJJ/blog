# Dockerfile

## 1. 简介

dockerfile是docker用来构建镜像的文本文件，包括自定义的指令和格式。可以通过`docker build` 命令从dockerfile中构建镜像。用户可以通过统一的语法命令来根据需求进行配置，通过这份统一的配置文件，在不同的文件上进行分发，需要使用时就可以根据配置文件进行自动化构建，这解决了开发人员构建镜像的复杂过程

## 2. 使用

dockerfile描述了组装对象的步骤，其中每条指令都是单独运行的。除了FROM指令，其他每条命令都会在上一条指令所生成镜像的基础上执行，执行完后会生成一个新的镜像层，新的镜像层覆盖在原来的镜像之上从而形成了新的镜像。dockerfile所生成的最终镜像就是在基础镜像上面叠加一层层的镜像层组建的