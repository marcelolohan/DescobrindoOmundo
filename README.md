import { useState, useEffect } from "react";
import { motion } from "framer-motion";

export default function App() {
  // Estado para controle da tela de suspense
  const [suspense, setSuspense] = useState(true);
  const [escolha, setEscolha] = useState("");
  
  // Função para avançar após o suspense (usando um timeout de 10 segundos)
  useEffect(() => {
    const timer = setTimeout(() => {
      setSuspense(false); // Muda para a tela de escolha após 10 segundos
    }, 10000); // 10 segundos de suspense
    return () => clearTimeout(timer); // Limpa o timer se o componente for desmontado
  }, []);

  const handleClick = (sexo) => {
    setEscolha(sexo); // Altera a escolha com base no botão clicado
  };

  return (
    <div className="min-h-screen flex flex-col items-center justify-center p-4">
      {/* Música de suspense */}
      <audio autoPlay loop>
        <source src="URL_DA_MUSICA_AQUI.mp3" type="audio/mp3" />
        Seu navegador não suporta áudio.
      </audio>

      {/* Tela de suspense */}
      {suspense ? (
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ duration: 1.5 }}
          className="text-center"
        >
          <motion.h1
            className="text-5xl font-bold text-gray-800 mb-6"
            animate={{ scale: [1, 1.2, 1] }}
            transition={{ duration: 2, repeat: Infinity, repeatType: "loop" }}
          >
            O momento está chegando...
          </motion.h1>
          <motion.div
            className="text-lg text-gray-600"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 1 }}
          >
            Aguarde a grande revelação!
          </motion.div>
        </motion.div>
      ) : (
        // Tela de escolha (Menino ou Menina)
        <>
          <motion.h1
            className="text-4xl md:text-6xl font-bold text-pink-600 mb-6"
            initial={{ opacity: 0, y: -50 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.8 }}
          >
            Em breve seremos três!
          </motion.h1>
          <motion.p
            className="text-lg text-gray-700 mb-8"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            transition={{ delay: 0.6 }}
          >
            A vida nos deu o maior presente que poderíamos receber...
          </motion.p>

          {/* Exibindo as opções de palpite */}
          {!escolha && (
            <div className="flex space-x-4">
              <motion.button
                whileHover={{ scale: 1.1 }}
                whileTap={{ scale: 0.9 }}
                className="bg-blue-500 text-white px-6 py-3 rounded-2xl shadow-lg"
                onClick={() => handleClick("Menino")}
              >
                💙 Vai ser Menino
              </motion.button>
              <motion.button
                whileHover={{ scale: 1.1 }}
                whileTap={{ scale: 0.9 }}
                className="bg-pink-500 text-white px-6 py-3 rounded-2xl shadow-lg"
                onClick={() => handleClick("Menina")}
              >
                💖 Vai ser Menina
              </motion.button>
            </div>
          )}

          {/* Exibindo a escolha feita */}
          {escolha && (
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ delay: 0.6 }}
              className="mt-8"
            >
              <h2 className="text-2xl font-semibold text-gray-800">
                Você escolheu: {escolha}
              </h2>
              <motion.div
                className="mt-4 text-xl text-gray-600"
                animate={{ rotate: 360 }}
                transition={{ duration: 1 }}
              >
                🎉 {escolha === "Menino" ? "Vamos ter um rapaz!" : "Vamos ter uma menina!"} 🎉
              </motion.div>
            </motion.div>
          )}
        </>
      )}
    </div>
  );
}
