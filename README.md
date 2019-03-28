pybtm
======

- [1 Installation](#1-installation)
- [2 Usage](#2-usage)
  - [2.1 Create entropy](#21-create-entropy)
  - [2.2 Create mnemonics](#22-create-mnemonics)
  - [2.3 Create seed](#23-create-seed)
  - [2.4 Create root expanded private key](#24-create-root-expanded-private-key)
  - [2.5 Create expanded public key](#25-create-expanded-public-key)
  - [2.6 Create expanded private key](#26-create-expanded-private-key)
  - [2.7 Create public key](#27-create-public-key)
  - [2.8 Create child expanded private key](#28-create-child-expanded-private-key)
  - [2.9 Create child expanded public key](#29-create-child-expanded-public-key)
  - [2.10 Sign message](#210-sign-message)
  - [2.11 Verify signature](#211-verify-signature)
  - [2.12 Create new key](#212-create-new-key)
  - [2.13 Create HD path](#213-create-hd-path)

Python3 implementation of the Bytom protocol.

## 1 Installation

```
$ pip install pybtm
```

## 2 Usage

### 2.1 Create entropy

get_entropy() create 128 bits entropy.

Return:

- entropy_hexstr: 128 bits entropy.

```python
>>> from pybtm import key
>>> key.get_entropy()
'100e2704b431f914e3262926bdba6fce'
```

### 2.2 Create mnemonics

get_mnemonic create 12 new mnemonics.

Parameter:

- entropy_hexstr(optional): 128 bits entropy, type is hex string.

Return:

- mnemonic_str: 12 mnemonics.

```python
>>> key.get_mnemonic('089fe9bf0cac76760bc4b131d938669e')
'ancient young hurt bone shuffle deposit congress normal crack six boost despair'
```

If no paramater is specified, it will return 12 new random mnemonics.

```python
>>> from pybtm import key
>>> key.get_mnemonic()
'nothing gate perfect glide wink lizard journey negative load quote wrong reason'
```

### 2.3 Create seed

get_seed create 512 bits seed from 12 mnemonics.

Parameter:

- mnemonic_str: 12 mnemonics.

Return:

- seed_hexstr: 512 bits seed, type is hex string.

```python
>>> from pybtm import key
>>> key.get_seed('ancient young hurt bone shuffle deposit congress normal crack six boost despair')
'afa3a86bbec2f40bb32833fc6324593824c4fc7821ed32eac1f762b5893e56745f66a6c6f2588b3d627680aa4e0e50efd25065097b3daa8c6a19d606838fe7d4'
```

### 2.4 Create root expanded private key

get_root_xprv create root expanded private key.

Parameter:

- seed_hexstr: 512 bits seed, type is hex string.

Return:

- root_xprv_hexstring: 512 bits seed, type is hex string.

```python
>>> from pybtm import key
>>> key.get_root_xprv('afa3a86bbec2f40bb32833fc6324593824c4fc7821ed32eac1f762b5893e56745f66a6c6f2588b3d627680aa4e0e50efd25065097b3daa8c6a19d606838fe7d4')
'302a25c7c0a68a83fa043f594a2db8b44bc871fced553a8a33144b31bc7fb84887c9e75915bb6ba3fd0b9f94a60b7a5897ab9db6a48f888c2559132dba9152b0'
```

### 2.5 Create expanded public key

get_xpub create expanded public key.

Parameter:

- xprv_hexstr: 512 bits expanded private key, type is hex string.

Return:

- xpub_hexstr: 512 bits expanded public key, type is hex string.

```python
>>> from pybtm import key
>>> xprv_hexstr = 'c003f4bcccf9ad6f05ad2c84fa5ff98430eb8e73de5de232bc29334c7d074759d513bc370335cac51d77f0be5dfe84de024cfee562530b4d873b5f5e2ff4f57c'
>>> key.get_xpub(xprv_hexstr)
'1b0541a7664cee929edb54d9ef21996b90546918a920a77e1cd6015d97c56563d513bc370335cac51d77f0be5dfe84de024cfee562530b4d873b5f5e2ff4f57c'
```

### 2.6 Create expanded private key

get_expanded_private_key create expanded private key.

Parameter:

- xprv_hexstr: 512 bits expanded private key, type is hex string.

Return:

- expanded_private_key_hexstr: 512 bits expanded private key, type is hex string.

```python
>>> from pybtm import key
>>> xprv_hexstr = '406c82307bf7978d17f3ecfeea7705370e9faef2027affa86c8027c6e11a8a50e231e65bd97048850ae6c39d0f46b63ae70aa24f5aac7877727c430c2201e6d6'
>>> key.get_expanded_private_key(xprv_hexstr)
'406c82307bf7978d17f3ecfeea7705370e9faef2027affa86c8027c6e11a8a50d828bf44b1a109c2bbb4c72685858e2f2ab8b405beef1e4ecc12d1ed8511e8eb'
```

### 2.7 Create public key

get_public_key create 32 bytes public key.

Parameter:

- xpub_hexstr: 512 bits expanded public key, type is hex string.

Return:

- public_key_hexstr: 256 bits public key, type is hex string.

```python
>>> from pybtm import key
>>> xpub_hexstr = 'ecc2bbb6c0492873cdbc81edf56bd896d3b644047879840e357be735b7fa7b6f4af1be7b8d71cc649ac4ca3816f9ccaf11bf49f4effb845f3c19e16eaf8bfcda'
>>> key.get_public_key(xpub_hexstr)
'ecc2bbb6c0492873cdbc81edf56bd896d3b644047879840e357be735b7fa7b6f'
```

### 2.8 Create child expanded private key

get_child_xprv create child private key.

Parameter:

- xprv_hexstr: 512 bits expanded private key, type is hex string.
- path_list: 010203 7906a1

Return:

- child_xprv_hexstr: 512 bits private key, type is hex string.

```python
>>> from pybtm import key
>>> xprv_hexstr = 'c003f4bcccf9ad6f05ad2c84fa5ff98430eb8e73de5de232bc29334c7d074759d513bc370335cac51d77f0be5dfe84de024cfee562530b4d873b5f5e2ff4f57c'
>>> path_list = ['010203', '7906a1']
>>> key.get_child_xprv(xprv_hexstr, path_list)
'4853a0b00bdcb139e85855d9594e5f641b65218db7c50426946511397e094759bd9de7f2dcad9d7d45389bc94baecaec88aabf58f6e1d832b1f9995a93ec37ea'
```

### 2.9 Create child expanded public key

get_child_xpub create child public key.

Parameter:

- xpub_hexstr: 512 bits expanded public key, type is hex string.
- path_list: 010203 7906a1

Return:

- child_xpub_hexstr: 512 bits public key, type is hex string.

```python
>>> from pybtm import key
>>> xpub_hexstr = '1b0541a7664cee929edb54d9ef21996b90546918a920a77e1cd6015d97c56563d513bc370335cac51d77f0be5dfe84de024cfee562530b4d873b5f5e2ff4f57c'
>>> path_list = ['010203', '7906a1']
>>> key.get_child_xpub(xpub_hexstr, path_list)
'e65c1a9714e2116c6e5d57dee188a53b98dc901a21def5a5ca46fcf78303f4f2bd9de7f2dcad9d7d45389bc94baecaec88aabf58f6e1d832b1f9995a93ec37ea'
```

### 2.10 Sign message

xprv_sign sign message.

Parameter:

- xprv_hexstr: 512 bits expanded private key, type is hex string.
- message_hexstr: message, type is hex string.

Return:

- signature_hexstr: 512 bits signature, type is hex string.

```python
>>> from pybtm import key
>>> xprv_hexstr = '88c0c40fb54ef9c1b90af8cce8dc4c9d54f915074dde93f79ab61cedae03444101ff37ac4a07869214c2735bba0175e001abe608db18538e083e1e44430a273b'
>>> message_hexstr = '1246b84985e1ab5f83f4ec2bdf271114666fd3d9e24d12981a3c861b9ed523c6'
>>> key.xprv_sign(xprv_hexstr, message_hexstr)
'ab18f49b23d03295bc2a3f2a7d5bb53a2997bed733e1fc408b50ec834ae7e43f7da40fe5d9d50f6ef2d188e1d27f976aa2586cef1ba00dd098b5c9effa046306'
```

### 2.11 Verify signature

xpub_verify verify signature.

Parameter:

- xpub_hexstr: 512 bits expanded public key, type is hex string.
- message_hexstr: message, type is hex string.
- signature_hexstr: 512 bits signature, type is hex string.

Return:

- result: True or False.

```python
>>> from pybtm import key
>>> xpub_hexstr = 'cb22ce197d342d6bb440b0bf13ddd674f367275d28a00f893d7f0b10817690fd01ff37ac4a07869214c2735bba0175e001abe608db18538e083e1e44430a273b'
>>> message_hexstr = '1246b84985e1ab5f83f4ec2bdf271114666fd3d9e24d12981a3c861b9ed523c6'
>>> signature_hexstr = 'ab18f49b23d03295bc2a3f2a7d5bb53a2997bed733e1fc408b50ec834ae7e43f7da40fe5d9d50f6ef2d188e1d27f976aa2586cef1ba00dd098b5c9effa046306'
>>> key.xpub_verify(xpub_hexstr, message_hexstr, signature_hexstr)
True
```

### 2.12 Create new key

get_new_key create new key.

Parameter:

- entropy_hexstr(optional): 128 bits entropy, type is hex string.
- mnemonic_str(optional): 12 mnemonics.

Return:

- entropy: 128 bits entropy.
- mnemonic: 12 mnemonics.
- seed: 512 bits seed.
- xprv: 512 bits expaneded private key.
- xpub: 512 bits expaneded public key.
- xprv_base64: xprv hex string qrcode base64.

```python
>>> from pybtm import key
>>> r = key.get_new_key()
>>> r['entropy']
'8466b1128f92051361c9aa2de52d1bb0'
>>> r['mnemonic']
'love culture dwarf busy cake meadow mango crystal combine city eight genuine'
>>> r['seed']
'4d15bf0f72bad754987fdcd0628ea37af03ac24666019c6d362e0200c9b49bee35aa0a788ed09e3a86cd529df0a1c20ea6aa719cf1e0da4ffb15efbc38fba498'
>>> r['xprv']
'f09ad64c2714b45e23c75e4541ad771def99b97e6da16b0cc6bcdac045f4d34745b62093173fd8f9a67e1da4b81233bc947880b6ed4b9641cf8f5223212fa18d'
>>> r['xpub']
'ebcc4b14444adb207dd53fd89b2881b21e839de42a1b6687a5a9d83b82c1b5b645b62093173fd8f9a67e1da4b81233bc947880b6ed4b9641cf8f5223212fa18d'
>>> r['xprv_base64']
{'base64': '/9j/4AAQSkZJRgABAQAAAQABAAD...'}
```

```python
>>> from pybtm import key
>>> r = key.get_new_key(entropy_hexstr='4d33735a9e92f634d22aecbb4044038d')
>>> r['entropy']
'4d33735a9e92f634d22aecbb4044038d'
>>> r['mnemonic']
'essay oppose stove diamond control bounce emerge frown robust acquire abstract brick'
```

```python
>>> from pybtm import key
>>> r = key.get_new_key(mnemonic_str='ancient young hurt bone shuffle deposit congress normal crack six boost despair')
>>> r['entropy']
''
>>> r['mnemonic']
'ancient young hurt bone shuffle deposit congress normal crack six boost despair'
>>> r['seed']
'afa3a86bbec2f40bb32833fc6324593824c4fc7821ed32eac1f762b5893e56745f66a6c6f2588b3d627680aa4e0e50efd25065097b3daa8c6a19d606838fe7d4'
```

### 2.13 Create HD path

get_path_from_index create HD path.

Parameter:

- account_index_int: 1, 2, 3, ..., type is hex string.
- address_index_int: 1, 2, 3, ..., type is hex string.
- change_bool: If receiver is change, change_bool is True, otherwise the change_bool is False.

Return:

- path_list: path list.
- path_str: path string.

```python
>>> from pybtm import receiver
>>> account_index_int = 1
>>> address_index_int = 1
>>> change_bool = True
>>> receiver.get_path_from_index(account_index_int, address_index_int, change_bool)
{'path': ['2c000000', '99000000', '01000000', '01000000', '01000000'], 'path_str': 'm/44/153/1/1/1'}
```
