## Juhend tegevusteks

Igale kasutajale on jagatud paber tema kasutajanime ja parooliga
1. Kasutades oma arvutis olevaid tööriistu, logi sisse masinasse 171.22.247.103
```shell
ssh <kasutajanimi>@171.22.247.103
 ```
2. kontrolli, kas ansible on olemas ja töötab:
```shell
ansible -version
```
3. Selleks, et Riigipilves ligi pääseda masinatele, mida sa oled loonud, on sul vaja panna kaasa on avalik võti,
mida sa kasutad sisselogimiseks. Selleks on kõigepealt vaja genereerida `ssh` võtmepaar:
```shell
ssh-keygen -b 2048 -t rsa
```
4. Logi sisse Riigipilve iseteenindusportaali - https://riigipliv.ee, ja impordi oma avalik võti enda
profiili alla. Selleks kuva oma avalik võti konsoolis,
```shell
cat ~/.ssh/id_rsa.pub
```
copy kuvatud võti clipboard -i ja pasteeri see Riigipilve iseteenindusportaali:

![img.png](readme_images/img.png)

Jäta aken lahti, sest seda läheb sul veel hiljem vaja

5. Lae alla Ansible nädisprojekt:
```shell
git clone --depth 1 https://github.com/riigipilv/ansible-demo.git
```
6. Asume uurima Ansible projekti struktuuri


7. Tekitame endale Ansible abiga Riigipilve om VM -i
 
```shell
~/ansible-demo/demo$ ansible-playbook -M /usr/local/lib/python3.8/dist-packages create_vm.yml
```
Script küsib Sinu käest ssh public võtme nime ja API tokenit.
Kui kõik läheb hästi ja vigu ei ole, siis saad Riigipilve UI -s vaadata, kas masin tekitati. Jäta masina juures meelde avalik IP

8. Installime veebi serveri

Uuendame faili `./invtory.site.yml` ja paneme sinna loodud masina IP aadressi
Jooksuta playbooki `install_webserver.yml`:
```shell
~/ansible-demo/demo$ ansible-playbook -i inventory/site.yml install_webserver.yml
```

