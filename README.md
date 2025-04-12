local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Espera a pasta "DanoQueda" aparecer no personagem
local function desativarDanoDeQueda()
    local tentativa = 0
    while tentativa < 10 do
        local danoQueda = character:FindFirstChild("DanoQueda")
        if danoQueda and danoQueda:IsA("Script") then
            danoQueda.Disabled = true
            print("[Anti Queda] Dano de queda desativado.")
            break
        end
        tentativa += 1
        wait(1)
    end
end

-- Caso o personagem respawnar, reativa a função
player.CharacterAdded:Connect(function(char)
    character = char
    desativarDanoDeQueda()
end)

desativarDanoDeQueda()
