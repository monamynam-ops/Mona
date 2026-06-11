library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Traffic_Light_Controller is
    Port (
        clk    : in STD_LOGIC;
        reset  : in STD_LOGIC;
        red    : out STD_LOGIC;
        yellow : out STD_LOGIC;
        green  : out STD_LOGIC
    );
end Traffic_Light_Controller;

architecture Behavioral of Traffic_Light_Controller is

type state_type is (GREEN_STATE, YELLOW_STATE, RED_STATE);
signal state : state_type := GREEN_STATE;

begin

process(clk, reset)
begin
    if reset = '1' then
        state <= GREEN_STATE;
    elsif rising_edge(clk) then
        case state is
            when GREEN_STATE =>
                state <= YELLOW_STATE;
            when YELLOW_STATE =>
                state <= RED_STATE;
            when RED_STATE =>
                state <= GREEN_STATE;
        end case;
    end if;
end process;

process(state)
begin
    case state is
        when GREEN_STATE =>
            green <= '1';
            yellow <= '0';
            red <= '0';

        when YELLOW_STATE =>
            green <= '0';
            yellow <= '1';
            red <= '0';

        when RED_STATE =>
            green <= '0';
            yellow <= '0';
            red <= '1';
    end case;
end process;

end Behavioral;   run this code
