Title: MUI の Button Group でドロップダウンを使用して分割する

Priority: 30

Button Group コンポーネントで Split Button(分割ドロップダウンボタン)を実装することができます。  
Split Button は、メインのアクションボタンと、他のオプションを選択できるドロップダウンメニューを持つボタンです。
ドロップダウンを使用して、ボタンのアクションを変更したり、関連するアクションをすぐにトリガーしたりできます。  

```tsx
import * as React from "react";
import Button from "@mui/material/Button";
import ButtonGroup from "@mui/material/ButtonGroup";
import ArrowDropDownIcon from "@mui/icons-material/ArrowDropDown";
import ClickAwayListener from "@mui/material/ClickAwayListener";
import Grow from "@mui/material/Grow";
import Paper from "@mui/material/Paper";
import Popper from "@mui/material/Popper";
import MenuItem from "@mui/material/MenuItem";
import MenuList from "@mui/material/MenuList";

// Split Button に表示される選択肢のリストを定義します
const options = [
  "Create a merge commit",
  "Squash and merge",
  "Rebase and merge",
];

export default function SplitButton() {
  // ドロップダウンメニューが開いているかどうかを管理する状態
  const [open, setOpen] = React.useState(false);
  // ボタンの位置を参照するための ref
  const anchorRef = React.useRef<HTMLDivElement>(null);
  // 現在選択されているオプションのインデックスを管理する状態
  const [selectedIndex, setSelectedIndex] = React.useState(1);

  // メインアクションボタンがクリックされたときに実行される関数
  const handleClick = () => {
    console.info(`You clicked ${options[selectedIndex]}`);
  };

  // メニューアイテムがクリックされたときに実行される関数。選択されたインデックスを更新し、メニューを閉じます
  const handleMenuItemClick = (
    event: React.MouseEvent<HTMLLIElement, MouseEvent>,
    index: number
  ) => {
    setSelectedIndex(index);
    setOpen(false);
  };

  // ドロップダウンボタンがクリックされたときにメニューの開閉をトグルする関数
  const handleToggle = () => {
    setOpen((prevOpen) => !prevOpen);
  };

  // メニューの外側がクリックされたときにメニューを閉じる関数
  const handleClose = (event: Event) => {
    if (
      anchorRef.current &&
      anchorRef.current.contains(event.target as HTMLElement)
    ) {
      return;
    }

    setOpen(false);
  };

  return (
    <React.Fragment>
      <ButtonGroup
        variant="contained"
        ref={anchorRef}
        aria-label="Button group with a nested menu"
      >
        <Button onClick={handleClick}>{options[selectedIndex]}</Button>
        <Button
          size="small"
          aria-controls={open ? "split-button-menu" : undefined}
          aria-expanded={open ? "true" : undefined}
          aria-label="select merge strategy"
          aria-haspopup="menu"
          onClick={handleToggle}
        >
          <ArrowDropDownIcon />
        </Button>
      </ButtonGroup>
      <Popper // ドロップダウンメニューを表示するためのコンテナ
        sx={{
          zIndex: 1,
        }}
        open={open}
        anchorEl={anchorRef.current}
        role={undefined}
        transition
        disablePortal
      >
        {({ TransitionProps, placement }) => (
          <Grow // メニューの表示にアニメーションを追加
            {...TransitionProps}
            style={{
              transformOrigin:
                placement === "bottom" ? "center top" : "center bottom",
            }} //
          >
            {/* メニューの背景 */}
            <Paper>
              {/* メニュー外のクリックを検出してメニューを閉じる */}
              <ClickAwayListener onClickAway={handleClose}>
                {/* メニューアイテムのリスト */}
                <MenuList id="split-button-menu" autoFocusItem>
                  {options.map((option, index) => (
                    <MenuItem
                      key={option}
                      disabled={index === 2}
                      selected={index === selectedIndex}
                      onClick={(event) => handleMenuItemClick(event, index)}
                    >
                      {option}
                    </MenuItem>
                  ))}
                </MenuList>
              </ClickAwayListener>
            </Paper>
          </Grow>
        )}
      </Popper>
    </React.Fragment>
  );
}
```

![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/e5b6d7fd-c140-4fe8-ad4b-278a34b6844e)


![image](https://github.com/mokelab/tech-sheets-contents/assets/37394133/fbab707f-f7ff-44fe-8ea9-41240ab268f9)
