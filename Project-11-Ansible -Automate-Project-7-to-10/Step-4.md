# RUN FIRST ANSIBLE TEST

Step 7 – Run first Ansible test

Now, it is time to execute ansible-playbook command and verify if your playbook actually works:

```
cd ansible-config-mgt
```

```
ansible-playbook -i inventory/dev.yml playbooks/common.yml
```

You can go to each of the servers and check if wireshark has been installed by running which wireshark or wireshark --version


![project-11111111](https://github.com/Amal-Suthan/DevOps_Projects/assets/64862440/79b9f96d-3de1-4f82-b716-bdbfc45b4516)


Your updated with Ansible architecture now looks like this:

![project-111111112](https://github.com/Amal-Suthan/DevOps_Projects/assets/64862440/e0617ee8-5dc3-42e2-850d-64e51da4842d)

![project-11](https://github.com/Amal-Suthan/DevOps_Projects/assets/64862440/ad7460dd-d51a-4003-a1e8-2c68009ee57a)

![project-11-1](https://github.com/Amal-Suthan/DevOps_Projects/assets/64862440/d37fb347-102a-4d9e-97f6-ac24532b43ea)

Optional step – Repeat once again
Update your ansible playbook with some new Ansible tasks and go through the full 
checkout -> change codes -> commit -> PR -> merge -> build -> ansible-playbook cycle again to see how easily you can manage a 
servers fleet of any size with just one command!

Congratulations
You have just automated your routine tasks by implementing your first Ansible project! There is more exciting projects ahead, so lets 
keep it moving!



