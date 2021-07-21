(in-package :stumpwm)

(run-shell-command "sh ~/.xprofile")

(setf *message-window-gravity* :center
      *input-window-gravity* :center
      *window-border-style* :thin
      *message-window-padding* 10
      *maxsize-border-width* 2
      *normal-border-width* 2
      *transient-border-width* 2
      stumpwm::*float-window-border* 4
      stumpwm::*float-window-title-height* 20
      *mouse-focus-policy* :click)

(run-shell-command "xmodmap -e 'clear mod4'" t)
(run-shell-command "xmodmap -e \'keycode 133 = F20\'" t)
(set-prefix-key (kbd "F20"))

(defvar *ce/workspaces* (list "WWW" "Code" "Term"))
(stumpwm:grename (nth 0 *ce/workspaces*))
(dolist (workspace (cdr *ce/workspaces*))
  (stumpwm:gnewbg workspace))

(defvar *move-to-keybinds* (list "!" "@" "#" "$" "%" "^" "&" "*" "("))
(dotimes (y (length *ce/workspaces*))
  (let ((workspace (write-to-string (+ y 1))))
    (define-key *root-map* (kbd workspace) (concat "gselect " workspace))
    (define-key *root-map* (kbd (nth y *move-to-keybinds*)) (concat "gmove-and-follow " workspace))))



(define-key *root-map* (kbd "Q") "quit")
(define-key *root-map* (kbd "R") "restart-hard")

(define-key *root-map* (kbd "q") "delete")
(define-key *root-map* (kbd "r") "remove")

(define-key *root-map* (kbd "h") "move-focus left")
(define-key *root-map* (kbd "j") "move-focus down")
(define-key *root-map* (kbd "k") "move-focus up")
(define-key *root-map* (kbd "l") "move-focus right")
(define-key *root-map* (kbd "H") "move-window left")
(define-key *root-map* (kbd "J") "move-window down")
(define-key *root-map* (kbd "K") "move-window up")
(define-key *root-map* (kbd "L") "move-window right")

(setf *resize-increment* 50)
(define-key *top-map* (kbd "M-l") "resize-direction Right")
(define-key *top-map* (kbd "M-h") "resize-direction Left")
(define-key *top-map* (kbd "M-k") "resize-direction Up")
(define-key *top-map* (kbd "M-j") "resize-direction Down")

(define-key *root-map* (kbd "RET") "exec st")
(define-key *root-map* (kbd "w") "exec brave")


(defun key-press-hook (key key-seq cmd)
  (declare (ignore key))
  (unless (eq *top-map* *resize-map*)
    (let ((*message-window-gravity* :bottom-right))
      (message "Keys: ~a" (print-key-seq (reverse key-seq))))
    (when (stringp cmd)
      ;; give 'em time to read it
      (sleep 0.3))))

(defmacro replace-hook (hook fn)
  `(remove-hook ,hook ,fn)
  `(add-hook ,hook ,fn))

(replace-hook *key-press-hook* 'key-press-hook)
