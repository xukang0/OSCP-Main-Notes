```
git clone https://github.com/dirkjanm/PKINITtools.git && cd PKINITtools
```

```
python3 -m venv .venv  && source .venv/bin/activate && pip3 install -r requirements.txt
```

If python script is lacking a module eg 

```
import aerospike
```

then

```
python3 -m venv venv
```

```
source venv/bin/activate
```

```
pip install aerospike
```
