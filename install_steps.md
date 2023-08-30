# How to run Lince-zero

```bash
git clone <repo>
cd <repo>
mkdir build
cd build
cmake ..
cd examples/falcon
make
cd  ../../
cd build/bin
./lince -h
./lince \
-m /content/modelos/models/lince-zero-f16-ggml-q4_0.bin \
-p "A continuación hay una instrucción que describe una tarea, junto con una entrada que\
proporciona más contexto. Escriba una respuesta que complete adecuadamente la solicitud.\n\n\
### Instrucctión:\nDame una lista de sitios a visitar en España\n\n### Respuesta:" \
-n 64