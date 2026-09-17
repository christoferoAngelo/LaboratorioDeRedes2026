# LaboratorioDeRedes2026 - Projeto Laboratório de Redes (Fatec Guarulhos)

Projeto final da disciplina **Laboratório de Redes**, simulando a infraestrutura de rede de uma empresa fictícia no **Cisco Packet Tracer**.

## Sobre o projeto

A empresa precisa de uma rede que atenda 4 departamentos — **Engenharia**, **Compras**, **TI** e **Infraestrutura** — cada um com 24 hosts (20 estações, 2 servidores e 2 impressoras), segmentados em VLANs, com topologia estrela, endereçamento Classe C (/27 por departamento) e acesso à internet para todos os equipamentos.

**Requisitos principais:**
- Rede Classe C, sub-redes `/27` (24 hosts), uma por departamento
- Topologia estrela
- 2 VLANs por departamento (12 portas cada: 1–12 e 13–24)
- Engenharia e TI com IP **estático** · Compras e Infraestrutura com IP **dinâmico** (DHCP)
- Switches de acesso Cisco 2960-24, todos interligados
- Todos os equipamentos com acesso à internet

## 🖧 Arquitetura

```
Internet (simulada)
        │
  Roteador ISP
        │
    Firewall (NAT)
        │
 Switch de Borda
        │
   Core Switch (L3 — roteamento entre VLANs + DHCP)
   ├── SW-Engenharia (VLAN 11 / 12)
   ├── SW-TI          (VLAN 21 / 22)
   ├── SW-Compras     (VLAN 31 / 32)
   └── SW-Infraestrutura (VLAN 41 / 42)
```

## 🌐 Endereçamento IP (resumo)

Rede base: `192.168.1.0/24`

| Departamento | Sub-rede | Máscara | 1º IP válido | Último IP válido | Broadcast |
|---|---|---|---|---|---|
| Engenharia | 192.168.1.0 | /27 | 192.168.1.1 | 192.168.1.30 | 192.168.1.31 |
| TI | 192.168.1.32 | /27 | 192.168.1.33 | 192.168.1.62 | 192.168.1.63 |
| Compras | 192.168.1.64 | /27 | 192.168.1.65 | 192.168.1.94 | 192.168.1.95 |
| Infraestrutura | 192.168.1.96 | /27 | 192.168.1.97 | 192.168.1.126 | 192.168.1.127 |

A tabela detalhada por VLAN (com gateway, faixa de PCs, servidor e impressora de cada uma) está em [`docs/tabela-ip.md`](docs/tabela-ip.md).

## 📁 Estrutura do repositório

```
.
├── README.md
├── packet-tracer/
│   └── supertech-rede.pkt          # arquivo principal do projeto
├── docs/
│   ├── tabela-ip.md                # tabela de IP completa (por VLAN)
│   ├── diagrama-rede.png           # print da topologia
│   └── configs/                    # configs de cada equipamento (CLI)
│       ├── core-switch.txt
│       ├── firewall.txt
│       ├── isp.txt
│       ├── sw-engenharia.txt
│       ├── sw-ti.txt
│       ├── sw-compras.txt
│       └── sw-infraestrutura.txt
└── evidencias/
    └── testes/                     # prints/vídeo da demonstração funcional
```

## ▶️ Como abrir

1. Instale o [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (versão 8.x ou compatível).
2. Abra o arquivo `packet-tracer/ProjetoRedes2026.pkt`.
3. As configurações de cada dispositivo podem ser conferidas na aba **CLI** de cada equipamento ou nos arquivos em `docs/configs/`.

## ✅ Testes realizados (demonstração funcional)

- [ ] PCs de Compras/Infraestrutura recebendo IP via DHCP na faixa correta
- [ ] Ping entre hosts da mesma VLAN
- [ ] Ping entre departamentos (roteamento inter-VLAN pelo Core Switch)
- [ ] Ping/acesso de qualquer host interno à internet simulada
- [ ] Acesso via navegador ao servidor externo (teste de NAT)

## 👥 Equipe

- Angelo C. Christofero
- Andrea L. Moraes

## 🏫 Disciplina

Laboratório de Redes — Fatec Guarulhos
Ambiente: Simulador Cisco Packet Tracer
