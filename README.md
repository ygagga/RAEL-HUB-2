local Redz = loadstring(game:HttpGet("https://raw.githubusercontent.com/RedzLibrary/Main/main/Redz.lua"))()

local ESP = Redz:NewESP({
    Enabled = true, -- Ativar ESP
    TeamCheck = false, -- Mostrar apenas inimigos (true) ou todos (false)
    Box = true, -- Caixa ao redor do jogador
    Name = true, -- Mostrar nome
    Health = true, -- Mostrar vida
    Distance = true, -- Mostrar distância
    Tracer = false, -- Linha até o jogador
    Highlight = true, -- Contorno ao redor do jogador
    Color = Color3.fromRGB(255, 0, 0) -- Cor do ESP (vermelho)
})

-- Função para adicionar jogadores ao ESP
local function UpdateESP()
    for _, player in pairs(game:GetService("Players"):GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            ESP:Add(player.Character)
        end
    end
end

-- Atualiza o ESP a cada segundo
task.spawn(function()
    while true do
        UpdateESP()
        task.wait(1)
    end
end)

-- Detecta novos jogadores e adiciona ao ESP
game:GetService("Players").PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        task.wait(1) -- Aguarda o personagem carregar
        UpdateESP()
    end)
end)
