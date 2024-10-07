-- Verifica se o serviço HttpService está habilitado
local HttpService = game:GetService("HttpService")

-- URL do script
local scriptUrl = 'https://raw.githubusercontent.com/Srmagnata99/Westbound/refs/heads/main/Westbound%20Elixir%20Client'

-- Função para carregar o script de forma segura
local function loadScript(url)
    local success, result = pcall(function()
        return HttpService:GetAsync(url)
    end)
    
    if success then
        local loadSuccess, loadResult = pcall(function()
            return loadstring(result)()
        end)
        
        if not loadSuccess then
            warn("Erro ao carregar o script: " .. loadResult)
        end
    else
        warn("Erro ao obter o script: " .. result)
    end
end

-- Função para aumentar o alcance da aura de mineração
local function aumentarAlcanceAura(miner)
    local originalRange = miner.AuraRange
    miner.AuraRange = originalRange * 3
end

-- Carrega o script
loadScript(scriptUrl)

-- Exemplo de uso da função de aumento de alcance
local miner = { AuraRange = 10 } -- Exemplo de objeto minerador
aumentarAlcanceAura(miner)
print("Novo alcance da aura de mineração: " .. miner.AuraRange)

