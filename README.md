# Jak utworzyć pull request na GitHub
Praca na zdalnym repozytorium w github.

## Klucze ssh

### Utwórz klucze ssh
Dodaj klucz publiczny breakermind.pub do swojego konta github w ustawieniach.
```sh
# Pliki kluczy
ssh-keygen -f ~/.ssh/breakermind -t ed25519 -b 521 -C "your-git-user@email.here"
ssh-keygen -f ~/.ssh/default-key-ecdsa -t ed25519 -b 521 -C "your-git-user@email.here"

# Prywatne klucze
ssh-add ~/.ssh/breakermind
ssh-add ~/.ssh/default-key-ecdsa

# Publiczny klucz do githuba
cat ~/.ssh/breakermind.pub
```

### Konfiguracja kluczy
nano ~/.ssh/config
```sh
# Ssh key breakermind
Host github.com
	HostName github.com    
	IdentityFile ~/.ssh/breakermind
	IdentitiesOnly yes
	# PreferredAuthentications publickey    
	# AddressFamily inet
	# User git  
	# Port 22

# Ssh, others
Host *
	IdentityFile ~/.ssh/default-key-ecdsa
	IdentitiesOnly yes
	# PreferredAuthentications publickey
	# AddressFamily inet
	# Protocol 2
	# Compression yes 
```

## Rozwój oprogramowania

### Ustawienia gita
```sh
git config --global user.name "Imię Nazwisko lub psełdonim"
git config --global user.email your-github-username@email.here
```

### Pobieranie kopii zdalnego repo na swoje konto github (fork repo)
Forknij zdalne repozytorium do którego chcesz dodać nową funkcjonalność.
```sh
git clone https://github.com/<username>/<repo-name>.git <dir-name>
```

### Utwórz nową funkcjonalność (gałąź) i dodaj jakiś plik z danymi
```sh
git checkout -b <branch-name>

touch file-1.txt
```

### Zatwierdź i wyślij zmiany do swojego repozytorium
```sh
git add .
git commit -am "Fix 1"

# Wyślij nową gałąź do swojego repozytorium github
git push -u origin <branch-name>

# Lub
git push --set-upstream origin <branch-name>
```

## Pull Request - Wyślij funkcjonalność (gałąź) do zdalnego repozytorium
Teraz można utworzyć Pull Request z własnego konta github dla funkcjonalności w forkniętym repozytorium i wysłać zmiany do zdalnego repozytorium w celu potwierdzenia zmian przez właściciela.

## Pobieranie zaktualizowanego zdalnego repozytorium
Zaakceptowanej przez właściciela zdalnego repozytorim zmiany nie ma na naszym forkniętym repo, dlatego trzeba dodać link do zdalnego repozytorium i pobrać z niego aktualne pliki.

### Dodanie zdalnego repozytorium
```sh
git remote add upstream https://github.com/<original-owner-username>/<original-repo>.git
git remote -v
```

### Uaktualnij lokalne repozytorim 
```sh
git fetch upstream/main

git checkout main

git merge upstream/main
```

### Wyślij zmiany na lokalne repozytorium github
```sh
git add .
git commit -m "Aktualizacja"
git push
```

# Cmd git
```sh
# Zmiana gałęzi
git checkout <branch-name>

# Na główną
git checkout main

# Dodaj pliki
git add .
git commit -am "Update"

# Lista zmian
git diff --staged
git diff --cached

# Wyślij
git push

# Pobierz
git pull
```

https://www.digitalocean.com/community/tutorials/how-to-create-a-pull-request-on-github
