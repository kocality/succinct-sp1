# Succinct SP1 ile Zero Knowledge Proof Doğrulama

<img src="https://app.ashbyhq.com/api/images/org-theme-wordmark/b045220d-46fa-4dd2-9364-ea30bc7bb174/81de4234-5c9f-40cf-8566-4324fd3a42f4.png" width="700"/>

## Succinct Hakkında
Succinct, blockchain uygulamalarını kriptografik doğrulukla güvence altına alarak merkeziyetsiz bir ağ inşa ediyor. Zero-knowledge proof (ZKP) sistemleri için güvenilir ve maliyet açısından verimli altyapı sunuyor.
* [Twitter](https://x.com/SuccinctLabs)
* [Website](https://succinct.xyz/)
* [Discord](https://discord.gg/succinctlabs)
* [Docs](https://docs.succinct.xyz/)
* [Github](https://github.com/succinctlabs)

## About SP1
SP1, programların doğru şekilde çalıştığını doğrulamak için zero-knowledge proof (ZKP) kullanan yüksek performanslı bir sanal makinedir (zkVM). Rust dilinde yazılmış kodlar kullanarak ZKP'leri kolayca uygulamanızı sağlar. Geleneksel ZKP sistemlerinin karmaşıklığını basitleştirerek, SP1 rollup'lar, köprüler ve light client'lar gibi çeşitli blockchain uygulamalarında güvenli ve hızlı çözümler sunar. Tamamen açık kaynaklı olan SP1, önde gelen blockchain projeleri tarafından güvenilmektedir ve düzenli güvenlik denetimlerine tabi tutulur.

SP1 hakkında daha fazla bilgi için [buraya bakabilirsiniz.](https://docs.succinct.xyz/introduction.html).

<img src="https://docs.succinct.xyz/sp1.png" width="700"/>

Not: Bu script yalnızca Ubuntu (20.04/22.04) üzerinde çalışır.


## Adım 1: Sistem Güncellemeleri ve Gerekli Araçların Kurulumu

### Sistem Paketlerini Güncelleyin
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install cmake pkg-config libssl-dev build-essential -y
```

### Rust ve Cargo Kurulumu
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

### Docker Kurulumu
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update >/dev/null 2>&1
sudo apt-get install -y docker-ce docker-ce-cli containerd.io >/dev/null 2>&1
sudo docker run hello-world >/dev/null 2>&1
```
#### Docker sürümünü kontrol edin:
```bash
docker --version
```

## Adım 2: SP1 Toolchain Kurulumu

### SP1'i İndirin ve Kurun
```bash
curl -L https://sp1.succinct.xyz | bash
source ~/.bashrc
sp1up
```

![1](https://github.com/user-attachments/assets/394f0326-56a0-4b78-928d-da591125d72a)


#### SP1'in doğru kurulduğundan emin olmak için sürümünü kontrol edin:
```bash
cargo +succinct --version
```

Adım 3: SP1 Projesini Başlatma ve Yapılandırma

### Yeni SP1 Projesi Başlatın
```bash
cargo prove new fibonacci
cd fibonacci/script
```

### Projeyi Çalıştırma ve Doğrulama (Not: Bu adım biraz zaman alabilir.)
```bash
# İlk olarak, her şeyin doğru şekilde kurulduğundan emin olmak için projeyi proof oluşturmadan çalıştırın:
RUST_LOG=info cargo run --release -- --execute

# Projenin başarılı bir şekilde çalıştığını doğruladıktan sonra ZKP oluşturun ve doğrulayın:
RUST_LOG=info cargo run --release -- --prove
```

#### SP1 CLI'nin başarılı bir şekilde kurulduğunu `cargo prove` sürümünü kontrol ederek doğrulayabilirsiniz:
```bash
cargo prove --version
```
![2](https://github.com/user-attachments/assets/c5a7d96a-779d-4669-b768-8f46906469ef)
