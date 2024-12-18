You can configure Ansible via a configuration file affecting the overall execution. For example, you can set the become password file globally so that you do not need to type it repeatedly when running Ansible.

The default configuration parameters should be sufficient for most users. However, there are some situations in which you might want to customize how Ansible operates.

The Ansible configuration is a file in defined in INI format, using a hash sign (`#`) for line comments and a semicolon (`;`) for line and inline comments. You can see an example in the following snippet, where the inventory source is set:

![[Pasted image 20241218201140.png]]

The Ansible configuration file can be set in different places and loaded in the following order:

- Set the ANSIBLE_CONFIG environment variable pointing out to the configuration file.
- ansible.cfg file created in the same directory where execute Ansible.
- ~/.ansible.cfg file located at the root of your home directory.
- /etc/ansible/ansible.cfg global file at the default Ansible directory.
